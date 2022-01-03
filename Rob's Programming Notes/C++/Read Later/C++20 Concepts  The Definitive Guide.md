---
link: https://thecodepad.com/cpp/c20-concepts-the-definitive-guide/
author: rajat
published: 2021-Aug-21T10:45:00
tags: []
---
# C++20 Concepts: The Definitive Guide
https://thecodepad.com/cpp/c20-concepts-the-definitive-guide/

![C++20 concepts logo](https://thecodepad.com/wp-content/uploads/2021/08/20-2-1024x576.jpg)

C++20 introduces concepts as a way to write powerful self-documenting templates. At their core, concepts are logical binary expressions that can be used to constrain the template parameters of any class or function template. These logical expressions are evaluated at compile time to determine whether the template parameters satisfy the given constraints.

The purpose of this tutorial is to be a definitive introduction point for C++20 concepts. It is split into 5 major sections:

1.  [A sample usage of pre-defined concepts in the standard library](#vs-static-assert)
2.  [How to write user-defined concepts](#user-defined-concepts)
3.  [Concepts’ participation in overload resolution as an alternative to SFINAE and `if constexpr`](#overloading)
4.  [Adding type constraints to `auto`](#constrained-auto)
5.  [Alternate ways to type constraint class/function templates](#more-syntax)

I also try to give simple code examples for each use case. Without further ado, let’s take a look at how a concept is defined in C++.

A named logical constraint is called a concept. The syntax for defining a concept is:

template<typename T, typename X...>
concept concept_name = <constraint>;

Before we delve deep into defining constraints and the benefits of concepts, let’s look at how to use them for an example C++ template function that adds integral types.

## C++17 static_assert vs C++20 concepts

In C++, constraints on type parameters can also be specified as static_assert statements inside a function call or class definition. A function that adds two integral types can look like this in C++17:

#include <type_traits>
template<typename T>
T add(T a, T b)
{
  static_assert(std::is_integral_v<T>);
  return a + b;
}

The above definition of `add` compiles only if `a` and `b` are integral types. For non-integral types, the compiler rightly throws the following error as static_assert fails.

test.cpp: In instantiation of ‘T add(T, T) [with T = std::basic_string<char>]’:
test.cpp:17:21:   required from here
test.cpp:11:22: error: static assertion failed
   11 |   static_assert(std::is_integral_v<T>);
      |                 ~~~~~^~~~~~~~~~~~~~~~
test.cpp:11:22: note: ‘std::is_integral_v<std::basic_string<char> >’ evaluates to false

Build finished with error(s).

Let’s now try to achieve the same behaviour with concepts. Like `[type_traits](https://en.cppreference.com/w/cpp/header/type_traits)`, the `[concepts](https://en.cppreference.com/w/cpp/concepts)` header contains many predefined concepts that can be used directly. For our purpose, we’ll use the [std::integral](https://en.cppreference.com/w/cpp/concepts/integral) concept. To constrain `typename T`, we simply replace `typename` with the name of the concept:

#include <concepts>
template<std::integral T>
T add(T a, T b)
{
  return a + b;
}

The above definition of `add` is equivalent to the one using static_assert. However, defining the function this way is self-documenting. Any user of the `add` function can look at the function signature and surmise that it will only work for integral types. For non-integral types, the error is:

test.cpp: In function ‘int main()’:
test.cpp:15:21: error: no matching function for call to ‘add(std::basic_string<char>, std::basic_string<char>)’
   15 |     std::cout << add("1"s,"2"s);
      |                  ~~~^~~~~~~~~~~
/home/rajat/cpp/test.cpp:8:3: note: candidate: ‘template<class T>  requires  integral<T> T add(T, T)’
    8 | T add(T a, T b)
      |   ^~~
test.cpp:8:3: note:   template argument deduction/substitution failed:
test.cpp:8:3: note: constraints not satisfied
In file included from test.cpp:1:
/usr/include/c++/11/concepts: In substitution of ‘template<class T>  requires  integral<T> T add(T, T) [with T = std::basic_string<char>]’:
test.cpp:15:21:   required from here
/usr/include/c++/11/concepts:102:13:   required for the satisfaction of ‘integral<T>’ [with T = std::basic_string<char, std::char_traits<char>, std::allocator<char> >]
/usr/include/c++/11/concepts:102:24: note: the expression ‘is_integral_v<_Tp> [with _Tp = std::basic_string<char, std::char_traits<char>, std::allocator<char> >]’ evaluated to ‘false’
  102 |     concept integral = is_integral_v<_Tp>;

Its a little verbose than the earlier implementation, but still manageable. Another alternative syntax to specify constraints is to use the requires keyword:

template<typename T> requires <constraint>
T add(T a, T b);

The `<constraint>` expression in a concept (or after requires) allows you to check for availability of operators, member functions, etc – something that is not possible with static_assert. Let us now look at how to write user-defined constraint expressions.

## Writing Constraint Expressions

If you look closely at the last line of the error in the previous section, you can see that `std::integral` is defined simply as:

template<typename _Tp>
concept integral = is_integral_v<_Tp>;

This is as simple as it can get. `[std::is_integral_v](https://en.cppreference.com/w/cpp/types/is_integral)` is a type trait defined in the type_traits header that evaluates to true if the template parameter is an integral type. C++ provides powerful operators in constraints expression that extend its functionality to check if:

1.  A statement can be compiled successfully
2.  A given type exists
3.  An instantiation of a template type is correct
4.  A function is non-throwing
5.  A function’s return type satisfies another concept
6.  A boolean expression evaluates to true

All of the above features are provided through the `requires` keyword. We’ll take a look at how to achieve each one of the above in the upcoming sections. But before that, let’s look at the syntax for requires expressions.

### Requires Expressions

The syntax of a requires expression is as follows:

requires (optional_parameter_list) { requirements; ...;}

The `optional_parameter_list` is a comma-separated list of parameters like a function definition. The variables specified in this list can just be used to assist in specifying compile time requirements and don’t have any lifetime, initialization, storage, etc. If no variables are required, the parentheses can be omitted. All subsections now look at how to specify `requirements` to achieve the functionalities specified in the previous section.

**Note:** This `requires` keyword works differently from the `requires <constraints>` expression we saw earlier while adding type constraints to `add`. This difference will become clearer as we discuss concepts in detail.

#### Checking if a statement can be compiled successfully

To check if a type parameter can be used as as intended by its class/function template, we can introduce a variable in the `optional_parameter_list` and write the intended usage as a `requirements` expression. In the example of the `add` template function above, if we want to allow the function to add any type that can be added, we can write the following concept:

template<typename T>
concept addable = requires (T a, T b) { a + b; };

The declaration of the `add` function will then become:

template<addable T>
T add(T a, T b);

It is imperative to note that the `a + b` in the requirements expression is not being executed; the compiler is only verifying if it can be compiled successfully. The `add` function is now able to add any two variables of the same type that can be added. It correctly (and succinctly) errors out when called with two cstrings:

test.cpp: In function ‘int main()’:
test.cpp:20:21: error: no matching function for call to ‘add(const char [2], const char [2])’
   20 |     std::cout << add("1", "2");
      |                  ~~~^~~~~~~~~~
test.cpp:11:3: note: candidate: ‘template<class T>  requires  addable<T> T add(T, T)’
   11 | T add(T a, T b)
      |   ^~~
test.cpp:11:3: note:   template argument deduction/substitution failed:
test.cpp:11:3: note: constraints not satisfied
test.cpp: In substitution of ‘template<class T>  requires  addable<T> T add(T, T) [with T = const char*]’:
test.cpp:20:21:   required from here
test.cpp:8:9:   required for the satisfaction of ‘addable<T>’ [with T = const char*]
test.cpp:8:19:   in requirements with ‘T a’, ‘T b’ [with T = const char*]
test.cpp:8:43: note: the required expression ‘(a + b)’ is invalid
    8 | concept addable = requires (T a, T b) { a + b; };
      |                                         ~~^~~

#### Checking if a type exists or if a template instantiation is correct

The `typename` keyword can be used in the `requirements` expression to ask the compiler to check whether a type is valid or if an instantiation of another class template satisfies the constraints imposed on it.

To check if a template parameter contains an `iterator_type` parameter:

template <typename T>
concept has_itertype = requires { typename T::iterator_type; };

Similarly, to check if an object can be placed in a vector:

template <typename T>
concept is_vectorizable = requires { typename std::vector<T>; };

#### Checking if a function is marked noexcept

To check if a function is marked noexcept, you need to use the following syntax for your `requirements` expression:

{ expression } noexcept;

Let’s create a `sub` function that uses `add` internally to perform `a - b`. We also add the requirement that `add` should be marked noexcept.

template <typename T>
concept subtractable = requires (T a) { { add<T>(a, a) } noexcept; a*-1; };

The above concept introduces three requirements:

1.  add<T> should be a valid template initialization
2.  add<T> should be marked noexcept
3.  Any object of type T should be multipliable by -1.

With these constraints, our `sub` definition becomes:

template<subtractable T>
T sub(T a, T b)
{
  return add(a, b*-1);
}

Since we did not mark `add` as noexcept in our previous examples, the following error is thrown when we try to subtract two integers:

test.cpp: In function ‘int main()’:
test.cpp:29:21: error: no matching function for call to ‘sub(int, int)’
   29 |     std::cout << sub(1, 2);
      |                  ~~~^~~~~~
test.cpp:20:3: note: candidate: ‘template<class T>  requires  subtractable<T> T sub(T, T)’
   20 | T sub(T a, T b)
      |   ^~~
test.cpp:20:3: note:   template argument deduction/substitution failed:
test.cpp:20:3: note: constraints not satisfied
test.cpp: In substitution of ‘template<class T>  requires  subtractable<T> T sub(T, T) [with T = int]’:
test.cpp:29:21:   required from here
test.cpp:17:9:   required for the satisfaction of ‘subtractable<T>’ [with T = int]
test.cpp:17:24:   in requirements with ‘T a’ [with T = int]
test.cpp:17:47: note: ‘add<int>(a, a)’ is not ‘noexcept’
   17 | concept subtractable = requires (T a) {{add<T>(a,a)} noexcept; a*-1;};
      |         

Once add is marked noexcept, the error disappears and the code compiles correctly.

#### Testing the return type of an expression

In the above (rather complicated) definition of `subtractable`, we also need to ensure that the return type of `add` and `a*-1` is `T`. If an object overrides `operator*` such that `a*-1` is not `T`, the template deduction for `add` will fail. On the other hand, if someone changes `add` such that the return type is no longer `T`, `sub` will fail to compile. The following syntax is used for checking testing return types:

{ expression } [noexcept] -> <constraint_expression>

The `constraint_expression` is usually another concept which can evaluate to true or false depending on the return type of `expression`. For our definition of `subtractable`, we’ll use `[std::same_as](https://en.cppreference.com/w/cpp/concepts/same_as)`.

template <typename T>
concept subtractable = requires (T a) { 
  {add<T>(a, a)} noexcept -> std::same_as<T>; 
  { a*-1 } -> std::same_as<T>;
};

The above concept now ensures that the return types of `add` and `a*-1` are `T`. One interesting thing to note is that `std::same_as` is a concept that accepts two template parameters and is defined as:

template < class T, class U >
concept same_as = /* impl */

However, in my usage above, I pass only one template argument. This is because C++ automatically fills the first template argument with the return type of `expression`.

#### Testing if boolean expressions evaluate to true

Until now, we have seen the requires `expression` only evaluate types and whether compilation of an expression would be successful. However, it is also possible to evaluate boolean expressions inside a `requires` requirements list. For evaluating logical expressions, the following syntax is used:

requires <boolean_expression>;

This may be confusing to see at first. Let’s look at a few examples to guage the difference. The following is concept checks if the size of the template parameter T is equal to 4.

template <typename T>
concept C1 = requires {requires sizeof(T) == 4;};

You may ask, what if we write it like this:  

template <typename T>
concept C2 = requires { sizeof(T) == 4; };

The difference between `C1` and `C2` is that `C2` doesn’t actually run `sizeof(T) == 4`. It just verifies whether the statement compiles. Therefore `C1<int_64t>` would return false, but `C2<int_64t>` would return true (since `8==4` is a valid expression).

Furthermore, it is also possible to write boolean expressions directly in the concept’s `constraint-expression` without the need for `requires`. A concept equivalent to `C1` can be written without `requires` like so:  

template <typename T>
concept C3 = ( sizeof(T) == 4 );

### Conjunctions in constraint-expressions

It is possible to conjugate constraint expressions using C++ logical operators for and/or/not. For example, the following concept constraints T to be both `addable` and `subtractable`.

template <typename T>
concept addable_and_subtractable = addable<T> and subtractable<T>;

## Overloading with C++ Concepts

Till now, we have seen how to define concepts and achieve better error messages and self-documenting function definitions. However, I think the most important point in favour of their usage is that they participate in overload resolution.

Let’s try to write a function `mul` that performs multiplication for two numbers. We also want `mul` to do a pythonic string multiplication where multiplying a string with an integer repeats the string that many number of times.

### Trying simple overloading without type constraints

We can define a template that multiplies two numbers of the same type and another that takes a templated type as the first argument and integer as the second. One such implementation can be:

template<typename T>
T mul(T a, T b)
{
  return a*b;
}

template<typename T>
T mul(T a, int b)
{
    std::string ret_val{std::move(a)};
    ret.reserve(ret_val.length() * b);
    auto start_pos{ret_val.begin()};
    auto end_pos{ret_val.end()};
    for(int i = 0; i < b; i++)
    {
        std::copy(start_pos, end_pos, std::back_inserter(ret_val));
    }
    return ret_val;
}

The first function takes two arguments of the same type, multiplies them, and returns the result. The second function takes any arbitrary type and an integer, it then converts the type to a string, performs the multiplication, and then casts the resulting string into the same type as the one that was passed before returning it.

However, it is not hard to see a problem with this. For `[T = int]`, the compiler will find two instantiations for the same function name and would throw an ambiguous function call error.

test.cpp: In function ‘int main()’:
test.cpp:48:21: error: call of overloaded ‘mul(int, int)’ is ambiguous
   48 |     std::cout << mul(1,10);
      |                  ~~~^~~~~~
test.cpp:29:3: note: candidate: ‘T mul(T, T) [with T = int]’
   29 | T mul(T a, T b)
      |   ^~~
test.cpp:35:3: note: candidate: ‘T mul(T, int) [with T = int]’
   35 | T mul(T a, int b)
      |   ^~~

Build finished with error(s).

### Using Concepts for overload resolution based on type

We can apply the `[std::convertible_to](https://en.cppreference.com/w/cpp/concepts/convertible_to)` concept to the second overload of `mul` so that the compiler picks ignores it when `mul` is called with `[T = int]`.

template<typename T>
T mul(T a, T b);

template<typename T> requires std::convertible_to<T, std::string> and std::convertible_to<std::string, T>
T mul(T A, int B);

The requires clause instructs the compiler to check if the passed type can be implicitly converted to std::string and vice-versa.

While not required for overload resolution, it would also be ideal to add a constraint on the first overload of `mul` to check if `a*b` is can be compiled and if its return type is the same as the template argument. This is left as an exercise to the reader.

### Benefits over SFINAE and `if constexpr`

A similar behaviour can be achieved with SFINAE and C++17’s `if constexpr`. With SFINAE, the two declarations can be changed to:

template<typename T>
T mul(T a, T b);

template<typename T>
std::enable_if_t<std::conjunction_v<std::is_convertible<T, std::string>, std::is_convertible<std::string, T>>, T> mul(T a, int b);

This achieves the exact same behaviour as our concept based implementation of `mul`. However, this is both harder to write and significantly less readable.

With `if constexpr`, we can create a python-like function that takes any argument and multiplexes between them on the basis of type. This can look like:

auto mul(auto a, auto b)
{
  if constexpr(std::is_convertible_v<decltype(a), std::string> and std::is_convertible_v<std::string, decltype(a)> and std::is_convertible_v<decltype(b), int>)
  {
    // String concatenation impl here
  } else if constexpr (std::is_same_v<decltype(a), decltype(b)>)
  {
    return a*b;
  }
}

This implementation is neat, but any user of the `mul` function would need to read the function definition in order to know what types of parameters are expected, and how they are used. Additionally, if the user passes a combination of parameters that don’t satisfy either `if constexpr` condition, the compiler would generate an empty `mul` function that returns `void` instead of throwing a compile time error.

### Participating in Overload Resolution

As seen in previous sections, functions can be overloaded with different type constraints. While resolving function overloads, the compiler expands each concept definition into its boolean form. It does so until a normalized boolean expression consisting of only conjunctions and disjunctions is formed.

Once all the concepts are resolved into a sufficiently simple boolean expression, the compiler picks the overload that with the most specific constraints. A constraint `A` is more specific than another constraint `B` if `A` implies `B`. The process of determining if a constraint implies another is called **Constraint Subsumption**. There are some caveats in **Constraint Subsumption** which are out of the scope of this article. If requested, I’ll add them as an addendum.

Let’s take a look at a simple example of overload resolution.

#include <concepts>
#include <iostream>

template<std::integral T>
void overloaded(T a)
{
   std::cout << "Integral overload called with " << a << std::endl;
}

template<std::integral T> requires (sizeof(T) == 2)
void overloaded(T a)
{
  std::cout << "Short overload called with " << a << std::endl;
}

int main()
{
  int a{10};
  short b{20};
  overloaded(a);
  overloaded(b);
}

The above example defines a function called `overloaded` with two different constraints. The first overload requires the template parameter `T` to be initialized to an integral type. The second overload places an additional condition on `T` that it must have a size of 2 bytes (If you are confused about the `sizeof(T)==2` syntax, jump to [this section](#more-syntax)). The function is then called with an `int` and a `short`. The output of the program is:

Integral overload called with 10
Short overload called with 20

It can be seen that the second call to `overloaded` satisfies constraints on both the overloads and the compiler picks the one that is the most specific.

**Note:** This overload resolution only works for function templates. If class template parameters are initialized such that they satisfy multiple concepts, the compiler throws a redeclaration error.

### Type constraining member functions of classes

Since template generation for member functions only happens when they are used, member functions can place tighter type constraints on the template variables. This way, parts of the class can be used by types that don’t satisfy a particular member function’s constraints as long as that member function remains unused. Let’s try this out with an example.

#include <concepts>
#include <iostream>

template<typename T>
struct Foo
{
  T a;
  std::string to_string() requires std::convertible_to<T, std::string>
  {
    return a;
  }
};

int main()
{
  Foo foo1{1}; // compiles
  Foo foo2{"abc"}; // compiles
  std::cout << foo2.to_string(); // prints "abc"
}

The above snippet of code compiles successfully even though `std::convertible_to<int, std::string>` returns false. However, this implies that `Foo<int>::to_string` can’t be called for foo1.

## Type constraining auto with concepts

The `auto` keyword in C++ can be type constrained with a concept. To do so, you need to preface the `auto` declaration with the name of the concept. For example:

std::unsigned_integral auto foo{1};

The above example constraints the type of `foo` to any unsigned integral type. Since foo is initialized to 1, which by default is a signed int, the compiler will throw an error for such a declaration.

This syntax can be used anywhere where `auto` keyword is allowed. Since C++20 allows for auto to be used as a type parameter, our `add` function that only adds integral values can look like:

std::integral auto add(std::integral auto a, std::integral auto b)
{
  return a + b;
}

It can also be used with lambdas:

auto add = [](std::integral auto a, std::integral auto b) { return a + b; };

If you want to use concepts that require more than one template parameter, you can assume that the first template parameter is filled by the deduced type of `auto` and provide the concept with all but the first template argument. Let’s correct the definition of `foo` provided at the start of the section by constraining its type to anything that is convertible to `unsigned int`:

std::convertible_to<unsigned int> auto foo{1};

## More ways to specify type constraints

There are a few more syntactical ways in which `requires <constraint>` can be specified for type-constraining class and function templates. Until now, we have limited the definition to logical expressions consisting of concepts. However, anything that can be written on the right hand side of the `=` operator while defining concepts can also be placed after the `requires` keyword.

Let us revisit the concept definition syntax:

template<typename T, typename X...>
concept concept_name = <constraint>;

The `<constraint>` expression can directly be substituted in place of `concept_name` in any occurrence of `requires concept_name`. This means that any `requires concept_name` can be written as `requires <constraint>`.

For example, our `add` function could’ve been declared as:

template<typename T> requires requires (T a, T b) { a + b; }
T add(T a, T b);

In the above example, we simply replaced `addable` with its definition.

Just to drive the point home, we also redefine `sub` by replacing the `subtractable` with its definition:

template<typename T> requires requires (T a) { { add<T>(a, a) } noexcept; a*-1; }
T sub(T a, T b);

This also shows that concepts are just a set of binary predicates that are evaluated at compile time.

Finally, for function templates, the `requires` keyword can also be specified after the function header. The following code also compiles fine:

template<typename T>
T add(T a, T b) requires addable<T>;

We saw the above syntax in the declaration of type-constrained class member functions.

## Conclusion

Phew, this was a long one. We discussed what concepts are, how to write them, and where they can be used. We also tried a few pre-defined concepts from the `concepts` header in C++20 and talked about how they participate in overload resolution.

The aim of this article was to provide the readers with a solid footing on C++20’s concepts and cover the most useful aspects that enable you to work with them. Your feedback would help me improve this article and add addendums with what you think is useful for new readers to start with templates.

If you are feeling up for some challenge, try to type constraint the `parse<T>` function in my post [“Performant String Parsing in C++”](https://thecodepad.com/cpp/performant-string-parsing-in-cpp/). And while you’re at it, overload the function for boolean types as well.

## Edits and Addendums

### Writing concepts for template parameter packs

It is possible to write concepts for template parameter packs with appropriate fold expressions. Let’s try to extend the `addable` concept to take a variable number of template parameters and return true only if all the template parameters are integral.

#include <concepts>

template<typename... Args>
concept addable = (std::integral<Args> and ...);

template<typename... Args> requires addable<Args...>
int add(Args... args)
{
  return (static_cast<int>(args) + ...);
}

The `add` function now takes a variable number of arguments, checks if all of them are integral, and returns their sum. Of course, we could’ve also used `std::integral` directly, like so:

#include <concepts>

template<std::integral... Args>
int add(Args... args)
{
  return (static_cast<int>(args) + ...);
}

Each template argument is now passed to `std::integral` individually and checked.

![](https://thecodepad.com/wp-content/uploads/2021/03/IMG-20200221-WA0012_Original.jpg)

rajat

### About the Author

I write code and chug tea while watching Netflix on my machine’s second screen. Currently trying to reverse engineer Iron Man’s discarded Mark 1 armour.

-   [](https://www.linkedin.com/in/rajatjain97/)
-   [](https://www.facebook.com/thecodepad)
-   [](https://www.instagram.com/thecodepad/)

The post [C++20 Concepts: The Definitive Guide](https://thecodepad.com/cpp/c20-concepts-the-definitive-guide/) appeared first on [The Code Pad](https://thecodepad.com).