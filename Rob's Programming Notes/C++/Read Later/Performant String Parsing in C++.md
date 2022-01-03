---
link: https://thecodepad.com/cpp/performant-string-parsing-in-cpp/
author: rajat
published: 2021-Aug-14T11:47:00
tags: []
---
# Performant String Parsing in C++
https://thecodepad.com/cpp/performant-string-parsing-in-cpp/

![Caterpiller parsing a string ](https://thecodepad.com/wp-content/uploads/2021/08/philippe-leone-IFAjplAqjos-unsplash-1024x684.jpg)

source: [Unsplashed](https://unsplash.com/photos/IFAjplAqjos)

Before C++17, the preferred way for parsing strings into arithmetic types was to use locale aware functions from standard library’s [stringstream](https://en.cppreference.com/w/cpp/header/sstream) or boost’s [lexical_cast](https://en.cppreference.com/w/cpp/header/sstream). In this post, we’ll discuss the [charconv](https://en.cppreference.com/w/cpp/header/charconv) header of the C++ standard library that was introduced in C++17 for performant parsing of cstrings and provide a zero-cost abstraction to leverage it for parsing `std::string` as well. This post is split into three sections:

1.  [Locale-aware high-level functions for parsing](#locale-aware-parsing)
2.  [The need for charconv and its features](#charconv)
3.  [A zero-cost wrapper over charconv to provide faster support for parsing strings](#parse-t)

## Locale-aware string parsing methods

Before discussing charconv, lets first take a look at the usage of conversion methods in the string header, stringstream, and lexical_cast for string parsing. All these methods are locale aware and differ ever so slightly so as to deserve their own section.

### Using conversion functions from string header

The string header exposes the following functions for numerical conversion of std::string to the required arithmetic type.

```cpp
int stoi( const std::string& str, std::size_t* pos = nullptr, int base = 10 );

long stol( const std::string& str, std::size_t* pos = nullptr, int base = 10 );

long long stoll( const std::string& str, std::size_t* pos = nullptr, int base = 10 );

float stof( const std::string& str, std::size_t* pos = nullptr)
...
```

There are similar functions for unsigned long, unsigned long long, double, long double, etc. These functions ignore leading whitespace, perform bounds checking, and throw exceptions if the conversion fails. The `pos` argument takes an optional pointer and sets it to the first unparsed character in the string. An example usage can be:

```cpp
#include <iostream>
#include <string>

int main()
{
  const std::string to_parse{"   123abc"};
  size_t index;
  int parsed_num{std::stoi(to_parse, &index)};
  std::cout << "Parsed Value: " << parsed_num << "\n";
  std::cout << "Unparsed character: " << to_parse[index] << "\n";
  return 0;
}
```

The output of the above program would be:

```
123
a
```

The third argument of stoi(), stol(), stoll(), and stoull() is an integral base. The default value assumes base 10 numbers. However, if base is set to 0, the functions use the following prefix notations to automatically figure out the base:

-   Numbers starting with `0X` and `0x` are treated as hexadecimal.
-   Number starting with `0` are treated as octal.
-   All other numbers are deserialised as decimal.

One disadvantage of this method is that these functions are not templatized on the return type and each have a different name. Thus, it results in a fragmented interface for the end user of the library. If the data that your library needs to parse changes from int to long int, you’ll need to replace all calls of stoi with stoll. The next two methods in this section circumvent the need to hardcode the function and instead choose it based on the type of output expected.

It also only works for std::string, therefore you’ll incur additional runtime penalty while casting cstrings to std::string. This behaviour is common in all three methods that I present in this section.

### Using std::istringstream for string parsing

[std::istringstream](https://en.cppreference.com/w/cpp/io/basic_istringstream) eschews the multiple methods approach from the string header conversion functions in favour of providing a stream type support for reading variables from strings. It works like anyone would expect a stream to work and ignores whitespace. However, contrary to the previous method, istringstream doesn’t throw when bounds check fail or casting isn’t possible. This error handling is left to the user.

```cpp
#include <iostream>
#include <sstream>

int main()
{
  std::string to_parse{"   123abc"};
  std::istringstream iss{to_parse};
  int num;
  iss >> num;
  std::cout << "Parsed number: " << num;
  return 0;
}
```

The output of the above program is:

```
123
```

However, since the stream operators don’t throw on error, users need to check for errors ourselves. The `good()` member function of the stream and be used to achieve this.

#include <iostream>
#include <sstream>

int main()
{
  std::string to_parse{"   79000abc"};
  std::istringstream iss{to_parse};
  short num;
  iss >> num;
  if (not iss.good())
  {
    std::cout << "There was some error in parsing!";
    return 1;
  }
  std::cout << "Parsed number: " << num;
  return 0;
}

The output of the above program is:

```
There was some error in parsing!
```

istringstream works well in most cases. In fact, boost::lexical_cast uses istringstream internally! The disadvantage of std::istringstream is that it is unwieldy to define a variable first, use it with `operator>>`, and then check for errors in the stream. Thus, for applications that do a fair bit of string parsing, the code would tend to grow long with similar patterns for casting everywhere.

However, since exceptions in C++ are considered fairly expensive for performance sensitive applications, `std::istringstream`‘s non throwing nature should give it a better performance in such use cases. The zero-cost abstraction for performant string parsing in the third section allows for both behaviours as a compile-time template parameter.

std::istringstream allows users to enable exceptions on errors. If you’re interested in how to achieve that, jump to [the end of this article](#stringstream-throw).

### Using boost::lexical_cast to condense std::stringstream usage

Boost’s lexical_cast is defined in <boost/lexical_cast.hpp>. It is a templated function that “casts” the provided string to the type provided as its template parameter. While doing so, it also performs bounds checking. The function throws exceptions if the parsing is unsuccessful or if the parsed number is out of bounds.

boost::lexical_cast does not, however, trim whitespaces. Unlike other methods in this section, it also expects the entire string to be consumed while parsing. If the entire string isn’t consumed, boost::lexical_cast throws an exception. In essence, it emulates python’s casts from string to arithmetic types. Let’s look at an example usage.

#include <iostream>
#include <boost/lexical_cast.hpp>

int main()
{
   auto num1{boost::lexical_cast<int>("123")};
   std::cout << num << std::endl;
   auto num2{boost::lexical_cast<int>("  456")}
   std::cout << num2 << std::endl;
   return 0;
}

The binary compiled from the above snippet would print 123 correctly but throw an exception while parsing “456”. This might not be acceptable while parsing user input.

The best thing about lexical_cast, in my opinion, is its concise syntax along with its ability to change the parsed string’s type as a template parameter. This allows for all the goodness of template code-generation to apply here. The abstraction implemented in this post uses a similar interface.

### Measuring run-time of locale-aware string parsing techniques

As a benchmark of comparison of each technique described above, I checked the number of instructions generated by each method when compiled with the -O3 flag on [godbolt.org](http://godbolt.org). While testing, I removed all the std::cout statements and added a return statement in main to return the parsed integer. The string parsed to parse was `"123"`. The results are below.

**Method**

**Lines of instructions**+**data**

**Number of** **Cycles**

String header methods

70

52.6

std::istringstream

41

35

boost::lexical_cast

392

313.2

Machine Code analysis of locale-aware string parsing techniques

It is possible to turn off locale awareness and use another function for numerical conversions from lexical_cast.hpp. This increases parsing performance significantly. To check the performance numbers, jump to [the end of the article](#try-lexical-convert).

Now that we know the numbers from each technique, its time to introduce charconv.

## charconv – C++’s low-level numerical conversion library

The C++17 standard introduces charconv, a low-library numerical conversion library with a focus on high-performance. All the functions defined in this header are non-allocating and don’t work directly with std::string. For converting numbers to strings, they require a pre-allocated buffer to be provided by the user. Similarly, for converting strings to numerical types, it takes as input the start and end of a character array. These functions are highly performant and can be used by high-throughput XML/JSON parsers as well.

Our functions of interest are the multiple overloads of [std::from_chars](https://en.cppreference.com/w/cpp/utility/from_chars). Their declarations are given below.

std::from_chars_result from_chars( const char* first, const char* last,
                                   IntType& value, int base = 10 )

std::from_chars_result from_chars( const char* first, const char* last,
                                   FloatType& value, chars_format  = 
                                   chars_format::general )

The first and second argument of from_chars take the start and end of the cstring. The third argument is an out parameter which returns value with the parsed numerical value. The integral overload also has a base argument that is similar to the one used by the numerical conversion methods in the string header. For floating types, the chars_format struct can be used to define the formatting of the string which needs to be converted. The formatting can be one of scientific, fixed, hex, or general. For more information on formatting, see the linked page on [cppreference](http://n cppreference: https://en.cppreference.com/w/cpp/utility/chars_format).

`std::from_chars_result` is a struct that contains a pointer to the unparsed string and an error code that indicates if the parsing has completed successfully.

For maximum performance, from_chars doesn’t trim whitespace and doesn’t recognise the ‘+’ character in front of positive integers – i.e. from_chars will parse “12” correctly, but will return an error for “+12”.

An interesting property of charconv is perfect round tripping. This means that converting a floating point value to string and then deserializing it back into a floating point variable yields the same exact same value that was used to serialize the string in the first place. To use perfect round tripping, you’ll need to use `std::to_chars` for serialization and `std::from_chars` for deserialization. I’ll reserve diving deep into perfect round tripping for a later time. For now, we are ready to wrap `std::from_chars` function with some zero-cost abstractions to make it intuitive to use in a larger codebase.

## parse<T> – A high performance string parser

We define two different modes of parsing:

-   **unsafe_parse**: A non-throwing parser. It returns a default value in case the parsing fails.
-   **safe_parse**: A throwing-parser. An exception is thrown if parsing fails and no default value is provided. Additionally, it trims whitespace and recognises the + sign in strings.

**unsafe_parse** and **safe_parse** are defined as follows:

#include <type_traits>
using safe_parse = std::false_type;
using unsafe_parse = std::negation<safe_parse>;

We also want to incorporate the advantages of all the three string parsing methods discussed above. These are:

1.  The string header methods make it easy to obtain the next pointer of the unparsed string.
2.  istringstream is non-throwing
3.  boost::lexical_cast has the most intuitive interface

Without further ado, below is my implementation of parse<T>:

#include <charconv>
#include <string_view>
#include <stdexcept>
#include <optional>

template<typename T, typename SAFE_PARSE_T=unsafe_parse>
[[nodiscard]] inline constexpr T parse(std::string_view sv, 
                                       const std::optional<T> default_val={}, 
                                       const char** next = nullptr)   
                                       noexcept(SAFE_PARSE_T::value)
{
  if constexpr(not SAFE_PARSE_T::value) {
    sv.remove_prefix(sv.find_first_not_of("+ ")); 
  }
  T var {default_val.value_or(T{})};
  auto ec = std::from_chars(sv.cbegin(), sv.cend(), var);
  if (next) *next = ec.ptr;
  if constexpr(not SAFE_PARSE_T::value) {
    if (default_val) {
      return var;
    }
    if(ec.ec!=std::errc{}) {
      throw std::runtime_error{"Parsing error!"};
    }
  }
  return var;
}

### Usage

The first argument can be constructed using std::string, cstring, or a pair of iterators. The second argument is the default value which should be returned in case of parsing errors. The third argument expects a pointer to a `const char*` and assigns it to the first character of the unparsed string.

It can be noted that the third argument could have been replaced with `std::optional<std::reference_wrapper<const char*>> next = {}`. This would ensure that whenever the third argument is specified in the parse function call, the result of the `if (next)` statement is always true. I was hoping that this hint would help the optimiser remove the branch statement at compile time. However, in my testing, gcc11 was smart enough to figure this out with `char**` as well and optimised away the branch cleanly.

The first template parameter is the type you want to parse the string as, and the second template parameter indicates whether the parse is should throw or not. An example usage can be:

#include <string>
#include <iostream>
int main()
{
  std::string to_parse{"   123abc"};
  const char* unparsed_str;
  auto parsed_num{parse<int, safe_parse>(to_parse, -1, unparsed_str};
  std::cout << "Parsed number: " << parsed_num << "\n";
  std::cout << "Unparsed string: " << unparsed_str << "\n"; 
  return 0;
}

The output of the above program is:

```
Parsed number: 123
Unparsed string: abc
```

We did not use unsafe_parse in the above example since the string to_parse contained whitespace as well.

### Explanation

First the function modifiers: I’ve used the `[[nodiscard]]` attribute to force the compiler to generate warnings in case a parsing result is discarded. `inline` and `constexpr` are self explanatory.

In unsafe mode, the function either does a zero-initialization or assigns the user provided default value to the result variable. Then it passes the variable to std::from_chars. After the parsing is complete, if the user has passed the next pointer to the function, it is initialized with the first character of the unparsed string. To detect errors in unsafe mode, the user can check the equality of the next pointer with the address of the first element of their string. The function then returns the parsed value to the user.

Safe mode has an added advantage of throwing a runtime error in case errors occur while parsing the user input. It should also be noted that safe_parse is not zero-cost as it contains a call to remove_prefix. For constant strings however, this is resolved at compile time. I think this is an ideal tradeoff. You can always remove it if it is an eyesore for you.

### Performance Numbers

I was thoroughly surprised while testing parse<T> on godbolt. For smaller strings, the parse function call is computed entirely at compile-time and the result of the computation is replaced at the place of the function call.

This code snippet:

int main()
{
  return parse<int>("10");
}

gets translated to:

```
main:
        mov     eax, 10
        ret
```

Awesome right?! In unsafe parsing mode, the compiler is also able to detect strings prefaced with whitespaces and appropriately returns the default value. In any case, for a fairer comparison, I made the string larger so as to force the compiler to generate code for the function. The stats for different inputs are as follows:

**Input**

**Number of instructions + data**

**Number of Cycles**

“10”

2

1.1

” 123″

2

1.1

“123”

35

8.4

“123abc”

35

8.4

Cycle count and number of instructions for parse<T, unsafe_mode>

As you can see, these numbers are much better than any of the approach discussed previously. Therefore, parse<T> can be used in fast path of latency sensitive applications where fast conversion from string values to numerical types is paramount.

## Conclusion

This implementation of parse<T> uses charconv under the hood to parse strings into numerical types in a performant manner. According to the benchmarks, parse<T> is much faster than other string parsing alternatives that are widely used. The implementation almost completely optimized out during compilation depending on the parsing mode picked.

This is my first article on [thecodepad](https://thecodepad.com/). I would love to hear your reviews and thoughts. If such content is helpful, I’ll keep writing. I’m open to feedback on how I can improve and what I should write on next. Thanks a lot for taking the time to read.

## Edits and Addendums

### Making std::istringstream throw on parsing errors

std::istringstream (and in general, all I/O streams in C++) have an exception mask that determines whether the stream throws on I/O errors or not. This mask can be toggled using [std::ios_base::exceptions](exceptions). A sample usage is:

#include <iostream>
#include <sstream>

int main()
{
  std::string to_parse{"70000"};
  short parsed_num{};
  std::istringstream ss{to_parse};
  ss.exceptions(std::istringstream::fail_bit);
  try
  {
    ss >> parsed_num;
  }
  catch(std::ios_base::failure& e)
  {
    std::cout << e.what() << std::endl;
    return 1;
  }
  std::cout << "Parsed number: " << parsed_num;
  return 0;
}

The output of the above program on clang 12 is:

```
ios_base::clear: unspecified iostream_category error
```

### Disabling lexical_cast’s exceptions and locale-awareness

boost::lexical_cast is performance tuned for a variety of use cases. It allows its users to turn off locale-awareness by defining the macro `BOOST_LEXICAL_CAST_ASSUME_C_LOCALE` before importing the header. In my tests, this brings down the cycle count by 50%.

Boost also provides a non-throwing alternative: `try_lexical_convert` in the namespace `boost::conversion`. Using this with `BOOST_LEXICAL_CAST_ASSUME_C_LOCALE` makes boost’s lexical_cast.hpp almost as performant as parse<T>. But before we see some numbers, here is an example usage.

#include <string>
#include <iostream>
#define BOOST_LEXICAL_CAST_ASSUME_C_LOCALE
#include <boost/lexical_cast.hpp>

int main()
{
  std::string to_parse{"123"};
  int parsed_num{};
  if(boost::conversion::try_lexical_convert<int>(to_parse, parsed_num))
  {
    std::cout << "Error while parsing!";
    return 1;
  }
  std::cout << "Parsed number: " << parsed_num;
  return 0;
}

Unlike lexical_cast, try_lexical_convert returns true on error and false if the parsing completes successfully. Instead, the second argument is treated as an output parameter and contains the result if parsing is successful. Another point to note is that it still requires the entire string to be consumed and doesn’t trim whitespaces. Let’s look at some performance numbers now!

**Input**

**try_lexical_convert**

**parse<T>**

“12”

7.4

2

“1234”

7.4

8.4

“80000000”

23.3

8.4

“80000000.001”

111.6

8.5

Number of cycles taken by each implementation for different inputs

From the results above, it can be seen that try_lexical_convert is a significant improvement over lexical_cast with locale awareness turned on. It can also be seen that parse<T> pulls ahead slightly for integer and significantly for double conversions. However, a significant advantage of try_lexical_cast is that it is available for all C++ standards starting from C++11.

![](https://thecodepad.com/wp-content/uploads/2021/03/IMG-20200221-WA0012_Original.jpg)

rajat

### About the Author

I write code and chug tea while watching Netflix on my machine’s second screen. Currently trying to reverse engineer Iron Man’s discarded Mark 1 armour.

-   [](https://www.linkedin.com/in/rajatjain97/)
-   [](https://www.facebook.com/thecodepad)
-   [](https://www.instagram.com/thecodepad/)

The post [Performant String Parsing in C++](https://thecodepad.com/cpp/performant-string-parsing-in-cpp/) appeared first on [The Code Pad](https://thecodepad.com).