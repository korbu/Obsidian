# C++ How to code string constants
**Created**: Tuesday, December 28, 2021 01:04:16 PM -05:00

Beginner or not, average (or not) C++ developer might think this is a non-issue. Nothing to talk about.

I would like to disagree.

I am pretty sure this “no-brainer” pulls a lot of legacy code and legacy thinking into the realm of your C++ code. Just a few short examples:

```cpp
// global char pointer

// C code actually

static const char * string_constant = "legacy code";


// "modern" "clever" C++ variant

// actually compiles to static const char *

// due to default handling of things in

// the anonymous namespaces

namespace {

    const char *

        string_constant = "legacy code";

}

// "standard" C++ ?

namespace maybe {

    // the naked char pointer is not very standard C++
    
    constexpr inline const char * string_constant
    
        = "naked pointer";
    
    // standard solution makes
    
    // for native char array
    
    // almost there ?
    
    constexpr inline const char
    
        string_constant_arr[]{"native char array" };
    
    // std string is a container,
    
    // not very light solution for
    
    // even a few constants of this sort
    
    inline const std::string
    
        string_constant_std{"wastefull"}

}
```

And so on and on. And yes more astute developers have interlaced the above “solutions” with a good and simple “lazy instantiation” idiom:

```cpp
// still a legacy solution

const char * get_the_string_constant ()

{

    // in standard C++ this is even
    
    // ok in the presence of multiple threads
    
    static const char * the_str_
    
        = "made once and not before needed";
    
    return the_str_ ;

}
```

A variant of the above, with more or much more C++ artifacts around it, is very often considered as the “ultimate”  solution to the application-wide string constants. And left as a such in the tons of running code worldwide.

## So what?

One might ask. Well, the first problem is this very often does not play well with standard C++.  Especially the naked pointer variant. Whenever the single native char pointer is delivered, one has to transform it into the `std::string` and then use it with standard C++ `std::algorithms`, utilities, and such.

```cpp
const char * whatever = get_the_string_constant ();

// just after this we can proceed using it

// with the std:: c++

const std::string the_user = whatever;

    for ( auto && element : the_user)
    
        { /* work here */ }

```

The above usage pattern is of course riddled with issues. So it is much better to copy the constant in these kinds of situations. Which is not very efficient.

A bit better solutions are not using C++17 or even 14 or 11, “goodies”. So they usually produce slower and heavier programs. Etc, etc …

By now I am sure you are “getting the picture”. Enough of this essay and let us jump straight into the

## Standard solution

```cpp
#include <string_view>

using namespace

::std::literals::string_view_literals;

namespace STANDARD {

    // make string view literal
    
    // will stay the same for the whole
    
    // application lifetime
    
    // will exhibit standard and expected interface
    
    // will be usable at both
    
    // runtime and compile time
    
    constexpr inline auto
    
        compiletime_string_view_constant
    
            = "compile time"sv ;

};
```

We use the standard C++ artifact: [string view](https://en.cppreference.com/w/cpp/string/basic_string_view/operator%22%22sv) literal. The standard string interface to the non-changeable native charr array. And equally importantly with value semantics.  Meaning moving/copying is implemented for us.

To involve this kind of constant into her modern C++ code, one does not need to transform it into anything. Just use it. It will be very resilient and safe to use too.

### Very quick test

```cpp
// test the resilience

auto return_by_val = []() {

    auto return_by_val = []() {

        auto return_by_val = []() {

            auto return_by_val = []() {

                return

STANDARD::compiletime_string_view_constant ;

            };

            return return_by_val();

        };

        return return_by_val();

    };

    return return_by_val();

};

// actually a run time

_ASSERTE(return_by_val().data() == "compile time");

// this is compile time artefact

static_assert(

    STANDARD::compiletime_static_string_view_constant

    == "compile time"

);
```

Yes, this solution is usable at both compile-time and runtime. Regardless of the fact it is not based on a fundamental type. (At least on my machine using CL Version 19.15.26726.0)

Here are the few “show-offs” using the `std::` c++ and this kind of a solution for application-wide string constants

```cpp
#include <string_view>

using namespace

::std::literals::string_view_literals;

// std artefacts conformance

auto the_constant =

    STANDARD::compiletime_static_string_view_constant;


// std interface allows this

// no need to extract the char *

// and or make the std string

_ASSERTE(the_constant == "compile time");


// make std init list

// from the first and last character

auto ref_w = {

    the_constant.front(),

    the_constant.back()

} ;

// make vector

const std::vector <char> vcarr{

    the_constant.data(),

    the_constant.data() + the_constant.size()

};

// standard interface has a `find` method

auto where = the_constant.find('e');

// and so on ...
```

Solution based on string views, will not enforce costly transformations in the client code and, god forbid, subtle bugs, creeping in with the use of char pointers or native char arrays.

Enjoy the standard C++. It is really not that difficult. Just make sure to leave the legacy behind.