# Beginner: Learn How to Program with C++

**Created**: Wednesday, March 28, 2018 11:46:55 PM -04:00
**Modified**: Tuesday, October 30, 2018 12:43:20 PM -04:00


https://app.pluralsight.com/library/courses/learn-programming-cplusplus/table-of-contents

#### 03/28/2018

# Pluralsight C++ Learning Path - Course # 1 of 12

1. Getting Started
    1. https://isocpp.org
    2. https://isocpp.org/get-started
    3. https://isocpp.org/tour
    4. [Programming: Principles and Practice Using C++ (2nd Edition): 0884926202607: Stroustrup, Bjarne: Books](https://smile.amazon.com/Programming-Principles-Practice-Using-2nd/dp/0321992784?sa-no-redirect=1)
    5. https://www.gregcons.com/kateblog/
2. Streams, Locals, and Flow of Control

(Finished)

#### 03/29/2018

3. Functions and Headers
    1. The auto keyword is like var in C#.
        1. Compiler figures out the variable's type.
    2. You cannot overload a function just by its return type.
        1. Many callers ignore the return type.
    3. When overloading, taking the same number of arguments but of different types is risky.
    4. Instead of an add function with 3 parameters returning a + b + c, do the following:
        1. <mark style="background: #BBFABBA6;">return add(add(a, b), c);</mark>
        2. i.e. use the 2 parameter version of add to return part of the three parameter version.
    5. Functions must be declared before they can be used.
    6. You can ***just*** put functions (***and nothing else***) into a .cpp file.
    7. Then you put ***just*** the declarations into the .h file.
    8. Then put `#include "Functions.h"` in your `main.cpp` file.
    9. The C++ Standard Library uses header file names with no extension, e.g. `<iostream>`.
        1. You don't need to have file extensions in your includes (or on your header file names).
    10. If you don't include a header file or if the function is not declared in the header, you will get a ***compiler error***.
    11. If you forget to implement the function, if the code for the function is not in the .cpp file, or if the .cpp file is not being linked, then you will get a ***linker error***.

Studied on the flight home

4. Strings and Collections
    1. Functions that are not class members are often referred to as free functions of non-member functions.
    2. Strings
        1`. #include <string>`
        2. For Unicode, use `wstring`.
        3. `cout << "hello" << endl;`
        4. `cin << name;`
            1. This lets you read space-separated parameters into variables.
            2. <mark style="background: #BBFABBA6;">If you type a number of parameters separated by spaces, they will each be treated as separate input.</mark>
            3. <mark style="background: #BBFABBA6;">This is how stream I/O works.</mark>
            4. Use the `getline` function instead if you want to capture all of a line's input as a single parameter.
        5. String operators:
            1. Combine two strings: + or +=
            2. Test two strings: == < > !=
            3. cout << and cin >> both work well with strings.
        6. String member functions:
            1. length, substr, find
    3. Collections
        1. `#include <vector>`
        2. `#include <algorithm> // for sort and count`
        3. `vector<int> vi;`
        4. `vi.push_back(i);`
        5. `vi.insert()` - use sparingly
        6. Ranged For:
            1. <mark style="background: #BBFABBA6;">for (auto item:vi) { }</mark>
        7. `vi.size()`
        8. Using iterators:

        ```c++
        for (auto i = begin(vi); i != end(vi); i++)
        
        {
        
        cout << *i << " ";
        
        }
        ```
        9. `sort (begin(vi), end(vi));`
        10. `int threes = count(begin(vi), end(vi), 3);`
        11. `int tees = count(begin(vs[0]), end(vs[0]), 't');`
5. Writing Classes
    1. Generally, member variables are private.
    2. Functions you think of early are usually public.
    3. Always initialize variables.
    4. <mark style="background: #BBFABBA6;">Any code that uses your class includes the header.</mark>
    5. <mark style="background: #BBFABBA6;">The .cpp file for the class includes the header.</mark>
    6. class { … code … };
        1. <mark style="background: #BBFABBA6;">Don't forget the semicolon at the end of a class definition.</mark>
    7. :: is the scope resolution operator.
    8. <mark style="background: #BBFABBA6;">Never use a namespace in a header file, e.g. `using namespace std;`.</mark>
        1. Reference types using `std::vector`, etc. in a header file.
        2. <mark style="background: #BBFABBA6;">Remember that a #include on a header essentially just pastes it into the .cpp file at compile time, so you may get unexpected results if you have using statements in your header files.  Don't do it.</mark>
        3. You can use the using statement in your .cpp files.
    9. In your .cpp files, you use `<class-name>::` before every function name, e.g. `Account::Account()`.
    10. You instantiate new instances of objects without using "new", e.g. `Transaction(amt, "Deposit");`
    11. <mark style="background: #BBFABBA6;">Use the to_string(balance) helper function.</mark>
        1. It is in the `std:: `namespace.
    12. "Inline Functions" are those you put in the header file rather than the .cpp file.
        1. They should really be functions that can fit on a single line, e.g. `int GetBalance() { return balance; }`
            > Continued on 04/02/2018
    13. Encapsulation
        1. Gives you freedom to change your class.
        2. <mark style="background: #BBFABBA6;">Make all member variables private.</mark>
        3. <mark style="background: #BBFABBA6;">Add public member functions as gatekeepers, e.g.` GetBalance()`.</mark>
        4. <mark style="background: #BBFABBA6;">Use as few public member functions as you can.</mark>
            1. <mark style="background: #BBFABBA6;">Use private functions if you want to keep from repeating code.</mark>
    14. A constructor that takes no arguments is the *default constructor*.
        1. `Account acct;`
        2. <mark style="background: #BBFABBA6;">BEWARE: `Account acct();` actually declares a function.</mark>
            1. Don't use this format to instantiate an Account.
    15. Declare objects with parameter-taking constructors using ().
        1. `Transaction t(amount, type);`
    16. Don't use = when declaring an object and initializing it.
    17. Remember to use destructors to clean up objects you've opened, e.g. file handles, database connections.
        1. RAII = [Resource acquisition is initialization](https://en.wikipedia.org/wiki/Resource_acquisition_is_initialization)
        2. Be careful with lifetime management.
        3. This is particularly important when you copy objects.
        4. Shared resources.
6. Compiler Specific Topics
    1. <mark style="background: #BBFABBA6;">#pragma once - tells the compiler to only include a header file once.</mark>
        1. Put it in `stdafx.h`.
7. Topics to Learn Later
            > 04/03/2018
    1. Casting
        1. Suppresses warnings.
        2. Makes your intent obvious.
        3. `int i = static_cast<int>(4.9);`
    2. The `const` keyword
        1. Expresses intent.
        2. Promises the compiler that a variable's value won't change.
            1. `const int amount = 90;`
        3. Promises that a member function won't change the values of any member variables.
            1. `string Transaction::Report() const { }`
            2. Add `const` to the function declaration and its definition.
        4. Make member functions and variables `const` as early as possible in the project.
        5. You may even want to consider making your functions `const` by default and then removing `const` later.
    3. The Standard Library
        1. If you need code to do something, check the Standard Library first.
        2. https://www.cplusplus.com/reference
    4. Passing Parameters
        1. By default, functions get a copy of the parameters you pass to them.
            1. <mark style="background: #BBFABBA6;">Think of those parameters as local variables.</mark>
            2. This is passing by value.
        2. To modify your parameters, you pass them by reference.
            1. `void foo(Transaction&amp; t);`
        3. <mark style="background: #BBFABBA6;">You also might not want to make a copy because it could be computationally expensive to do so.</mark>
            1. If you don't want to have the passed by reference parameter be modifyable, add `const`.
            2. `void foo(const Transaction&amp; t);`
            3. <mark style="background: #BBFABBA6;">This also expresses intent.</mark>
8. Legacy Constructs