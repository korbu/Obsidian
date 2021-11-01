# C++ Move Semantics

by *Nicolai M. Josuttis*

My progress through the overview and all 15 chapters: <progress value="3" max="16"></progress>

> This book covers all aspects of C++ move semantics up to C++20.

## The Key to Move Semantics

You can **steal** the value of an object by "moving" the ownership of its memory. It is not a technical move, it is a semantic move.

## Overview

Example code files for the book can be found at <https://www.cppmove.com/>.

* Browse the code at <https://cppmove.com/code/basics/>.

Please use the following email address for feedback: [cppmove@josuttis.com](mailto:cppmove@josuttis.com)

## Part I: Basic Features of Move Semantics

This part of the book introduces the basic features of move semantics that are **not** speciﬁc to generic programming (i.e., templates). They are particularly helpful for application programmers in their day-to-day programming and therefore every C++ programmer using Modern C++ should know them. This starts in [[Chapter 01]].

Move semantics features for generic programming are covered in Part II (see [[Chapter 09]].

### Use the modern form of initialization (introduced in C++11 as _uniform initialization_) with curly braces

```c++
#include <iostream>

// Example # 1
int i{42};

// Example # 2
// j is guaranteed to be 0.
int j{};

// Example # 3
std::string s{"hello world"};

std::cout << "int i = " << i << "\n";
std::cout << "int j = " << j << "\n";
std::cout << "string s = " << s << "\n";

// Example # 4
// It detects narrowing errors.
// int j{31.5};

// Example # 5
// Initialize a container with multiple values, also known as aggregate initialization.
// - Also see https://en.cppreference.com/w/cpp/language/aggregate_initialization.
// - Note: You are better off using std::array than regular C/C++ arrays here.
int k[]{ 1, 2, 4, 8 };

// Display all of the elements from that array using a range-based for loop.
for (int element : k) {
    std::cout << element << " ";
}
```

> See <https://compiler-explorer.com/z/G8jq7Pbao> to try the above code.

Also called _brace initialization_, it has the following advantages:

1. It can be used with:
	1. fundamental types,
	2. class types,
	3. aggregates,
	4. enumeration types, and
	5. `auto`.  
2. It can be used to ==initialize containers with multiple values==.
	1. Also see https://en.cppreference.com/w/cpp/language/aggregate_initialization.
	2. `TODO`: Try this in the compiler.
	3. `TODO`: Add an example to Compiler Explorer.
3. It can detect ==narrowing errors== (e.g., initialization of an `int` by a floating-point value).
	1. See the example in the code, above.
	2. `TODO`: Try this in the compiler.
4. It cannot be confused with function declarations or calls.  

If the ==braces are empty==, the default constructors of (sub)objects are called and fundamental data types are guaranteed to be initialized with `0`/`false`/`nullptr`.

#### Initializing a class with empty braces

```c++
#include <iostream>

class Apple
{
protected:
    int seeds;

public:
    Apple()
    {
    }
    
    Apple(int seedCount)
    {
        seeds = seedCount;
    }
    
    int GetSeeds()
    {
        return seeds;
    }
};

// Initialize an object with empty braces and integer members are initialized to 0.
// - Note: VS2019 returned garbage instead of 0 and displayed a warning that it was uninitialized.
// TODO: Try this in VS2022 and see if the same behavior occurs.
Apple myApple{};
std::cout << "Number of seeds = " << myApple.GetSeeds() << "\n";

Apple anotherApple{5};
std::cout << "Number of seeds = " << anotherApple.GetSeeds() << "\n";
```

> See <https://compiler-explorer.com/z/x389fvGKc> to try the above code.

### Header Files

All header files should have something like the following:

```c++
#ifndef MYFILE_HPP
#define MYFILE_HPP
...
#endif // MYFILE_HPP
```

Previous: [[_Overview]]
Next: [[Chapter 02]]