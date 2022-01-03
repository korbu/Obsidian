# Section 01 - Bikeshedding is bad
**Created**: Tuesday, December 28, 2021 12:24:07 PM -05:00

## Chapter 1.1: P.2 Write in ISO Standard C++
[C++ Core Guidelines (isocpp.github.io)](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#p2-write-in-iso-standard-c)

<mark style="background: #FFF3A3A6;">TODO: </mark>[A History of C++: 1979− 1991 (stroustrup.com)](https://www.stroustrup.com/hopl2.pdf)

### Handling variations in run-time environments
Do not use the following:

```c++
#if defined WIN32
auto a_pressed = bool{GetKeyState('A') & 0x8000 != 0}
#elif defined LINUX
auto a_pressed = /* really quite a lot of code */
#endif
```

This is very ugly: it is operating at the wrong level of abstraction. The code that is specific to Windows and Linux should live in separate files elsewhere, exposed in a header file, so the code should look like this:

```c++
auto a_pressed = key_state('A');
```

The function `key_state` is an interface that encapsulates this extension. Take it out of your flow of control and **without the additional baggage of preprocessor macros**.

### Handling variations in C++ language level and compiler
GCC included additional type traits such as `__has_trivial_constructor` and `__is_abstract` before they were added to the C++ standard.  These have both been present in the type traits library since C++11 under different names: `std::is_trivially_constructible` and `std::is_abstract`.

Note that `__is_abstract` is preceded by a double underscore: <mark style="background: #BBFABBA6;">the double underscore is reserved by the C++ standard for implementers</mark>.  Implementers are **NOT** allowed to add new identifiers to the standard namespace, i.e., `std::`.

A good way to guard against accidentally using compiler-specific features is to <mark style="background: #BBFABBA6;">build and test your code on more than one compiler and operating system</mark> to discover accidentally non-standard code.

### Safety in header files
Consider `#pragma once`.  This is a simple directive that reduces the amount of time the compiler spends compiling a translation unit.  But what does it actually mean?

1. Does it mean "stop parsing until you get to the end of the file"?
2. Does it mean "don't open this file a second time"?

Although the visible effect is the same, the meaning is not precisely defined for all platforms.

You cannot assume the meaning of something will be preserved across platforms.  Even if you are safe now, you cannot guarantee that you will be in the future.  Relying on a feature like this is like relying on a bug.  It's dangerous and may be changed or corrected at any time.  Although, see [Hyrum's Law (hyrumslaw.com)](https://www.hyrumslaw.com/):

_An observation on Software Engineering_

Put succinctly, the observation is this:

> With a sufficient number of users of an API,  
> it does not matter what you promise in the contract:  
> all observable behaviors of your system  
> will be depended on by somebody.

>![[Pasted image 20211228151152.png ]]
>"There are probably children out there holding down spacebar to stay warm in the winter! YOUR UPDATE MURDERS CHILDREN."
>[xkcd: Workflow](https://xkcd.com/1172/)

In this case, rather than using `#pragma once`, the Core Guidelines recommend using header guards as described in SF.8: Use `#include` guards for all `.h` files [C++ Core Guidelines (isocpp.github.io)](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#sf8-use-include-guards-for-all-h-files).

> **SF.8**: In order to avoid include guard collisions, do not just name the guard after the filename. Be sure to also include a key and good differentiator, such as the name of library or component the header file is part of.

#### SF.8 Example:

```c++
// file foobar.h:
#ifndef LIBRARY_FOOBAR_H
#define LIBRARY_FOOBAR_H
// ... declarations ...
#endif // LIBRARY_FOOBAR_H
```

> **SF.8 Note**: Some implementations offer vendor extensions like `#pragma once` as alternative to include guards. It is not standard and it is not portable. It injects the hosting machine’s filesystem semantics into your program, in addition to locking you down to a vendor. Our recommendation is to write in ISO C++: See [rule P.2](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rp-Cplusplus).

### Handling variation  in fundamental types
The width of arithmetic types like `int` and `char` is not standardized.  Instead of assuming that `int` would always be 32-bits wide, the author used the implementation heads to discover which type was that wide and created an alias to that type:

```c++
typedef __int i32; // old way of doing this; do not use this now.
```

In C++11, new types were introduced to the library in header `<cstdint>` that defined fixed-width integral types.  He was then able to update the definition to:

```c++
using i32 = std::int32_t; // #include <cstdint>
```

> Note: This enabled him to move to the new `using` keyword, which allows you to use left-to-right style for identifier and definition separated by an equals sign.  You can also see this style with the `auto` keyword:

```c++
auto index = i32{0};
```

The identifier is introduced on the left of the equals sign and the definition is on the right side of the equals sign.

However, a better solution was to swap all of his instances of i32 with `std::int32_t` for minimum ambiguity (**since C++11**).

Also see [Fixed width integer types (since C++11) - cppreference.com](https://en.cppreference.com/w/cpp/types/integer), [Type support (basic types, RTTI, type traits) - cppreference.com](https://en.cppreference.com/w/cpp/types), and [Fundamental types - cppreference.com](https://en.cppreference.com/w/cpp/language/types).

### Backward compatibility of C++ and Forward compatibility and "Y2K"
An important part of career skills is writing code for the future and learning to read code from the past.

### Staying on top of developments to the standard
With every publication of a new C++ standard there comes aa cornucopia of new language features and library additions.  The C++ community is very fortunate to have many excellent teachers ready to unfold and reveal all these new things to us.  Finding these resource is made easier in four ways:

#### IsoCpp: [Standard C++ (isocpp.org)](https://isocpp.org/)
This is the home of C++ on the Web and is run by the Standard C++ Foundation.  On this site, you can find a tour of C++ by Bjarne Stroustrup ([Tour : Standard C++ (isocpp.org)](https://isocpp.org/tour)), a huge C++ FAQ ([C++ FAQ (isocpp.org)](https://isocpp.org/faq)), and a regularly updated list of recent blog posts from the C++ community ([Blog : Standard C++ (isocpp.org)](https://isocpp.org/blog).

#### Conferences
1. [CppCon | The C++ Conference](https://cppcon.org/): Held in Aurora, CO in early Autumn.
    1. [CppCon - YouTube](https://www.youtube.com/user/CppCon)
2. [ACCU Conference](https://accu.org/conf-main/main/): Held in the Spring in Bristol, UK
    1. [ACCU Public Magazine: Overload Content by Issue (accu.org)](https://accu.org/journals/nonmembers/overload_issue_members/)
    2. [ACCU Member-Only Magazine: C Vu Content by Issue (accu.org)](https://accu.org/journals/nonmembers/cvu_issue_neutered/)
    3. [Membership Information (accu.org)](https://accu.org/menu-overviews/membership/)
    4. [ACCU Conference - YouTube](https://www.youtube.com/c/ACCUConf/featured)
3. [Meeting C++ (meetingcpp.com)](https://meetingcpp.com/): Held in November in Berlin, Germany
    1. [Meeting Cpp - YouTube](https://www.youtube.com/user/MeetingCPP/videos)

#### Other resources
1. Blogs
2. Books
3. Chat Servers, such as Discord and Slack.
    1. Slack: https://cpplang.slack.com
    2. Discord: https://www.includecpp.org
        1. [Join Discord (includecpp.org)](https://www.includecpp.org/discord/)

## Chapter 1.2: Where there is a choice, prefer default arguments over overloading.
