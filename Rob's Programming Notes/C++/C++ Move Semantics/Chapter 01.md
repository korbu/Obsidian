# C++ Move Semantics

by *Nicolai M. Josuttis*

My progress through all 15 chapters: <progress value="2" max="15"></progress>

> This book covers all aspects of C++ move semantics up to C++20.

## The Key to Move Semantics

You can **steal** the value of an object by "moving" the ownership of its memory. It is not a technical move, it is a semantic move.

## Overview

Example code files for the book can be found at <https://www.cppmove.com/>.

* Browse the code at <https://cppmove.com/code/basics/>.

Please use the following email address for feedback: [cppmove@josuttis.com](mailto:cppmove@josuttis.com)

## Part I: Basic Features of Move Semantics

This part of the book introduces the basic features of move semantics that are **not** speciﬁc to generic programming (i.e., templates). They are particularly helpful for application programmers in their day-to-day programming and therefore every C++ programmer using Modern C++ should know them.

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

1. It can be used with fundamental types, class types, aggregates, enumeration types, and `auto`.  
1. It can be used to <mark>initialize containers with multiple values</mark>.
   1. Also see https://en.cppreference.com/w/cpp/language/aggregate_initialization.
   2. TODO: Try this in the compiler.
1. It can detect <mark>narrowing errors</mark> (e.g., initialization of an `int` by a floating-point value).  
   1. TODO: Try this in the compiler.
1. It cannot be confused with function declarations or calls.  

If the <mark>braces are empty</mark>, the default constructors of (sub)objects are called and fundamental data types are guaranteed to be initialized with `0`/`false`/`nullptr`.

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

## Chapter 1: The Power of Move Semantics

### 1.1 Motivation for Move Semantics

To understand the basic principles of move semantics, let us look at the execution of a small piece of code,
first without move semantics (i.e., compiled with an old C++ compiler that supports only C++03) and then
with move semantics (compiled with a modern C++ compiler that supports C++11 or later).

### 1.1.1 Example with C++03 (Before Move Semantics)

Note that the same behavior would happen with any C++ compiler that does not support move semantics.

```c++
// Example with C++03 (Before Move Semantics)

#include <string>
#include <vector>

std::vector<std::string> createAndInsert()
{
    std::vector<std::string> coll; // create vector of **strings** (on the stack)
    coll.reserve(3);               // reserve memory for 3 **elements** (on the heap)
    std::string s ="data";         // create string **object** (on the stack)
    
    coll.push_back(s);             // insert string object
    coll.push_back(s+s);           // insert temporary string
    coll.push_back(s);             // insert string
    
    return coll;                   // return vector of strings
}

std::vector<std::string> v;        // create empty vector of **strings** (on the stack)

//...

v = createAndInsert();             // assign returned vector of strings
```

### How the above code works

1. First, in main(), i.e. outside the function, we create the empty vector v:

```c++
std::vector<std::string> v;
```

   which is placed on the stack as an object that has 0 as the number of elements and no memory allocated for elements.
   
2. Then, we call

```c++
v = createAndInsert();
```

   where we create another empty vector `coll` on the stack and reserve memory for three elements on the heap:
   
```c++
std::vector<std::string> coll;
coll.reserve(3);
```
   
The allocated memory is not initialized because the number of elements is still 0.

3. Then, we create a string initialized with "data":

```c++
std::string s ="data";
```

A string is something like a `vector` with `char` elements. Essentially, we create an object on the stack
with a member for the number of characters (having the value 4) and a pointer to the memory for the
characters.

After this statement, the program has the following state: we have three objects on the stack: `v`, `coll`,
and `s`. Two of them, `coll` and `s`, have allocated memory on the heap.

The next step is the command to insert the string into the vector coll:

```c++
coll.push_back(s);
```

### All containers in the C++ standard library have value semantics, which means that they create copies of the values passed to them.

As a result, we get a ﬁrst element in the vector, which is a full (deep) copy of the passed value/object `s`.

![image-01.png](image-01.png)

So far, we have nothing to optimize in this program. The current state is that we have two vectors, `v` and `coll`, and two strings, `s` and its copy, which is the ﬁrst element in coll. They should all be separate objects with their own memory for the value, because modifying one of them should not impact any of the other objects.

4. Let us now look at the next statement, which creates a new temporary string and again inserts it into the vector:

```c++
coll.push_back(s+s);
```

This statement is performed in three steps:

1. We create the **temporary** string s+s.
1. We insert this **temporary** string into the vector coll. As always, the **container creates a copy** of the passed value, which means that we create a deep copy of the temporary string, including allocating memory for the value.
1. At the end of the statement, the temporary string `s+s` is destroyed because we no longer need it:

![image-02.png](image-02.png)

Here, we have the <mark>ﬁrst moment where we generate code that is not performing well</mark>: we create a copy of a temporary string and destroy the source of the copy immediately afterwards, which means that we unnecessarily allocate and free memory that **we could have just moved from the source to the copy**.

5. With the next statement, again we insert `s` into `coll`:

```c++
coll.push_back(s);
```

Again, `coll` copies `s`:

![image-03.png](image-03.png)

This is also something to improve: because the value of `s` is no longer needed some optimization could use the memory of s as memory for the new element in the vector instead.

6. At the end of createAndInsert() we come to the return statement:

```c++
   return coll;
}
```

Here, the behavior of the program becomes a bit more complicated. <mark>We return by value (the return type is not a reference)</mark>, which should be a copy of the value in the return statement, `coll`. Creating a copy of `coll` means that we have to create a deep copy of the whole vector with all of its elements. Thus, we have to allocate heap memory for the array of elements in the vector and heap memory for the value each string allocates to hold its value. Here, we would have to allocate memory 4 times.

However, since at the same time `coll` is destroyed because we leave the scope where it is declared, the compiler is allowed to perform the named return value optimization (NRVO).

### Named return value optimization

NRVO means that the compiler can generate code so that `coll`, a local variable on the stack in a method, is just used as the return value instead of destroying the local copy and returning another copy of it. <mark>This optimization is allowed even if this would change the functional behavior of the program.</mark>

If we had a print statement in the copy constructor of a vector or string, we would see that the program no longer has the output from the print statement. <mark>This means that this optimization changes the functional behavior of the program. However, that is OK, because we explicitly allow this optimization in the C++ standard even if it has side effects.</mark> Nobody should expect that a copy is done here, in the same way that nobody should expect that it is not, either. It is simply up to the compiler whether the named return value optimization is performed.

Let us assume that we have the named return value optimization. In that case, at the end of the return statement, `coll` now becomes the return value and the <mark>destructor</mark> of `s` <mark>is called</mark>, which frees the memory allocated when it was declared:

![image-04.png](image-04.png)

7. Finally, we come to the assignment of the return value to `v`:

```c++
v = createAndInsert();
```

Here, we really get behavior that can be improved: the usual assignment operator has the goal of giving `v` the same value as the source value that is assigned. In general, any assigned value should not be modiﬁed and should be independent from the object that the value was assigned to. So, <mark>the assignment operator will create a deep copy of the whole return value (in C++03)</mark>:

![image-05.png](image-05.png)

However, right after that, we no longer need the temporary return value and we destroy it:

![image-06.png](image-06.png)

Again, we create a copy of a temporary object and destroy the source of the copy immediately afterwards,
which means that we again unnecessarily allocate and free memory. This time it applies to four
allocations, one for the vector and one for each string element.

For the state of this program after the assignment in `main()`, we allocated memory ten times and released it
six times. The unnecessary memory allocations were caused by:

1. Inserting a temporary object into the collection
1. Inserting an object into the collection where we no longer need the value
1. Assigning a temporary vector with all its elements

### Avoiding performance penalties in C++03

We can more or less avoid these performance penalties (in C++03). In particular, instead of the last assignment, we
could do the following:

```c++
// Improved example with C++03 (Before Move Semantics)
// - The same behavior would happen with any C++ compiler that does not support move semantics.

#include <string>
#include <vector>

std::vector<std::string> createAndInsert(std::vector<std::string> coll)
{
    coll.reserve(3);               // reserve memory for 3 **elements**
    std::string s ="data";         // create string **object**
    
    coll.push_back(s);             // insert string object
    coll.push_back(s+s);           // insert temporary string
    coll.push_back(s);             // insert string

    std::cout << "Length of vector = " << coll.size() << "\n";
    
    return coll;                   // return vector of strings
}

std::vector<std::string> v;        // create empty vector of **strings**
std::cout << "Length of vector = " << v.size() << "\n";

// Pass the vector as an out parameter:
//createAndInsert(v.swap(v)); // let the function fill vector v
//std::cout << "Length of vector = " << v.size() << "\n";

// Use swap():
// TODO: ERROR! This cannot work, as the return type of createAndInsert is now void. Emailed Nico on 04/26/2021 to ask how to
//       correctly implement this version.
//createAndInsert().swap(v);
```

<mark>However, the resulting code looks uglier</mark> (unless you see some beauty in complex code) and there is not
really a workaround when inserting a temporary object.

Since C++11, we have another option: compile and run the program with support for move semantics.

### 1.1.2 Example Since C++11 (Using Move Semantics)

Let us now recompile the program with a modern C++ compiler (C++11 or later) that supports move semantics:

**File**: basics/motiv11.cpp (http://cppmove.com/code/basics/motiv11.cpp.html)

```c++
#include <string>
#include <vector>

std::vector<std::string> createAndInsert()
{
  std::vector<std::string> coll;  // create vector of strings (on the stack)
  coll.reserve(3);                // reserve memory for 3 elements (on the heap)
  std::string s = "data";         // create string object (on the stack)

  coll.push_back(s);              // insert string object
  coll.push_back(s+s);            // insert temporary string
  coll.push_back(std::move(s));   // insert string (we no longer need the value of s) ** Note the std::move(s) **

  return coll;                    // return vector of strings
}

std::vector<std::string> v;     // create empty vector of strings

//...

v = createAndInsert();          // assign returned vector of strings

//...
```

There is a small modiﬁcation, though: we add a `std::move()` call when we insert the last element into `coll`. We will discuss this change when we come to this statement. Everything else is as before.

Again, let us look at the individual steps of the program by inspecting both the stack and the heap.

1. First, in `main()`, we create the empty vector `v`, which is placed on the stack with 0 elements:

```c++
std::vector<std::string> v;
```

2. Then, we call

```c++
v = createAndInsert();
```

where we create another empty vector `coll` on the stack and reserve uninitialized memory for three elements on the heap:

```c++
std::vector<std::string> coll;
coll.reserve(3);
```

3. Then, we create the string s initialized with "data" and insert it into coll again:

```c++
std::string s = "data";
coll.push_back(s);
```

So far, there is nothing to optimize and we get the same state as with C++03:

![image-07.png](image-07.png)

We have two vectors, `v` and `coll`, and two strings, `s` and its copy, which is the ﬁrst element in `coll`. They should all be separate objects with their own memory for the value, because modifying one of them should not impact any of the other objects.

4. This is where things change. First, let us look at the statement that creates a new temporary string and inserts it into the vector:

```c++
coll.push_back(s+s);
```

Again, this statement is performed in three steps:

1. We create the temporary string `s+s`:

![image-08.png](image-08.png)

2. We insert this temporary string into the vector `coll`. However, <mark>here something different happens now</mark>: we steal the memory for the value from `s+s` and move it to the new element of `coll`.

![image-09.png](image-09.png)

<mark>This</mark> is possible because since C++11, we can implement special behavior for getting a value that is no longer needed. The compiler can signal this fact because it knows that right after performing the `push_back()` call, the temporary object `s+s` will be destroyed. So, <mark>we call a different implementation of `push_back()` provided for the case when the caller no longer needs that value.</mark> As we can see, the effect is an optimized implementation of copying a string where we no longer need the value: instead of creating an individual deep copy, we copy both the size and the pointer to the memory. However, that shallow copy is not enough; <mark>we also modify the temporary object `s+s` by setting the size to `0` and assigning the `nullptr` as new value.</mark> Essentially, `s+s` is modiﬁed so that it gets the state of an empty string. The important point is that <mark>it no longer owns its memory.</mark> And that is important because we still have a third step in this statement.

3. At the end of the statement, <mark>the temporary string `s+s` is destroyed because we no longer need it</mark>. However, because the temporary string is no longer the owner of the initial memory, <mark>the destructor will not free this memory.</mark>

![image-10.png](image-10.png)

<mark>Essentially, we optimize the copying so that we move the ownership of the memory for the value of `s+s` to its copy in the vector.</mark>

This is all done automatically by using a compiler that can signal that an object is about to die, so that we can use new implementations to copy a string value that steals the value from the source. <mark>It is not a technical move; it is a semantic move implemented by technically moving the memory for the value from the source string to its copy.</mark>

5. The next statement is the statement we modiﬁed for the C++11 version. Again, we insert `s` into `coll`, but the statement has changed by calling `std::move()` for the string `s` that we insert:

```c++
coll.push_back(std::move(s));
```

<mark>Without `std::move()`, the same would happen as with the ﬁrst call of `push_back()`: the vector would create a deep copy of the passed string `s`.</mark> However, in this call, we have marked `s` with `std::move()`, which **semantically** means <mark>**_"I no longer need this value here."_**</mark> As a consequence, we have another call of the other implementation of `push_back()`, which was used when we passed the temporary object `s+s`.

The third element <mark>steals the value by moving the ownership of the memory for the value from `s` to its copy:</mark> (**This is the key to move semantics!!!**)

![image-11.png](image-11.png)

Note the following two very important things to understand about move semantics:

1. <mark>`std::move(s)` only **_marks_** `s` to be movable in this context. It does not move anything.</mark> It only says, "**_I no longer need this value here_**." It allows the implementation of the call to benefit from this mark by performing some optimization when copying the value, such as stealing the memory. Whether the value is moved is something the caller does not know.

   1. That **mark** is an `&&`. This will be covered later.

2. However, an optimization that steals the value has to ensure that the source object is still in a valid state. A moved-from object is neither partially nor fully destroyed. The C++ standard library formulates this for its types as follows: after an operation called for an object marked with `std::move()`, the object is in a **_valid but unspeciﬁed state_**.

That is, after calling

```c++
coll.push_back(std::move(s));
```

it is guaranteed that `s` is still a valid string. You can do whatever you want as long as it is valid for any string where you do not know the value. <mark>It is like using a string parameter where you do not know which value was passed.</mark>

Note that it is also not guaranteed that the string either has its old value or is empty. The value it has is up to the implementers of the (library) function. In general, implementers can do with objects marked with `std::move()` whatever they like, provided they leave the object in a valid state. There are good reasons for this guarantee, which will be discussed later (i.e. in Section 2.3).

6. Again, at the end of `createAndInsert()` we come to the return statement:

```c++
  return coll;
}
```

It is still up to the compiler whether it generates code with the _named return value optimization_ which would mean that `coll` just becomes the return value. However, if this optimization is not used, the return statement is still cheap, because again we have a situation where we create an object from a source that is about to die. That is, <mark>if the named return value optimization is not used, move semantics will be used, which means that the return value steals the value from `coll`.</mark> At worst, we have to copy the members for size, capacity, and the pointer to the memory (in total, usually 12 or 24 bytes) from the source to the
return value and assign new values to these members in the source.

Let us assume that we have the named return value optimization. In that case, at the end of the return statement, `coll` now becomes the return value and the destructor of `s` is called, which no longer has to free any memory because it was moved to the third element of `coll`:

![image-12.png](image-12.png)

7. So, ﬁnally, we come to the assignment of the return value to `v`:

```c++
v = createAndInsert();
```

Again, we can beneﬁt from move semantics now because we have a situation we have already seen: we have to copy (here, assign) a value from a temporary return value that is about to die.

Now, move semantics allows us to provide a different implementation of the assignment operator for a vector that just steals the value from the source vector:

![image-13.png](image-13.png)

Again, the temporary object is not (partially) destroyed. It enters into a valid state but we do not know its value.

However, right after the assignment, <mark>the end of the statement destroys the (modiﬁed) temporary return value:</mark>

![image-14.png](image-14.png)

At the end we are in the same state as before using move semantics but something signiﬁcant has changed: <mark>we saved six allocations and releases of memory.<mark> All unnecessary memory allocations no longer took place:

1. Allocations for inserting <mark>a temporary object</mark> into the collection
2. Allocations for inserting <mark>a named object</mark> into the collection, when we use `std::move()` to signal that we no longer need the value
3. Allocations for assigning <mark>a temporary vector</mark> with all its elements

In the second case, the optimization was done with our help. By adding `std::move()`, we had to say that we no longer needed the value of `s` there. All other optimizations happened because the compiler knows that an object is about to die, meaning that it can call the optimized implementation, which uses move semantics.

<mark>This means that returning a vector of strings and assigning it to an existing vector is no longer a performance issue. We can use a vector of strings naively like an integral type and get much better performance.</mark> In practice, recompiling code with move semantics can improve speed by 10% to 40% (depending on how naive the existing code was).

### Technical vs. Semantic Moves (reviewing the content above)

In C++11 (and later), we call a different implementation of `push_back()` provided for the case when the caller no longer needs the value of a variable. Instead of creating an individual deep copy, we copy both the size and the pointer to the memory.

However, that shallow copy is not enough; we also modify the temporary object `s+s` by setting the size to 0 and
assigning the `nullptr` as its new value. Essentially, `s+s` is modified so that it gets the state of an empty string. The important point is that it no longer owns its memory.

At the end of the statement, the temporary string `s+s` is destroyed because we no longer need it. However, because the temporary string is no longer the owner of the initial memory, the destructor will not free this memory.

It is not a **technical move**; it is a **semantic move** implemented by technically moving the memory for the value from the source string to its copy. **Temporary variables can be stolen to eliminate a copy.**

### std::move()

Marking a variable with `std::move()` semantically means "I no longer need this value here." It steals the value by moving the ownership of the memory for the value from the variable to its copy. **`std::move` steals memory to eliminate a copy.**
    
### Two Key Points about Move Semantics

Two very important things to understand about move semantics:

1. `std::move(s)` **only marks s to be movable** in this context. **It does not move anything.** It only says, "I no longer need this value here." It allows the implementation of the call to benefit from this mark by performing some optimization when copying the value, such as stealing the memory. Whether the value is moved is something the caller does not know.

1. However, an optimization that steals the value has to ensure that the source object is still in a valid state. A moved-from object is neither partially nor fully destroyed. The C++ standard library formulates this for its types as follows: **after an operation** called for an object marked with std::move(), **the object is in a valid but unspecified state.**

### 1.2 Implementing Move Semantics

Since C++11, we have a second overload of push_back():

```c++
template<typename T>
class vector {
   public:
   ...
   // insert a copy of elem:
   void push_back (const T& elem);

   // insert elem when the value of elem is no longer needed:
   void push_back (T&& elem);
   ...
};
```

The second `push_back()` uses a new syntax introduced for move semantics. <mark>We declare the argument with two `&` and without `const`.</mark> Such an argument is called an ***rvalue reference***.

"Ordinary references" that have only one `&` are now called ***lvalue references***. That is, in both calls we pass the value to be inserted by reference.

However, the difference is as follows:

* With `push_back(const T&)`, we promise not to modify the passed value. This function is called when the <mark>caller still needs the passed value</mark>.

* With `push_back(T&&)`, <mark>the implementation can modify the passed argument (therefore it is not const) to "steal" the value</mark>. The semantic meaning is still that the new element receives the value of the passed argument but we can use an optimized implementation that moves the value into the vector.
    * This function is called <mark>when the caller no longer needs the passed value</mark>. The implementation has to ensure that the passed argument is still in a valid state. However, the value may be changed. Therefore, after calling this, the caller can still use the passed argument as long as the caller does not make any assumption about its value.

### 1.2.2 Using the Move Constructor

`push_back(T&&)` for the new move semantics calls a corresponding new constructor, the ***move constructor***.

This is the constructor that creates a new string from an existing string, where the value is no longer needed.

As usual with move semantics, the constructor is declared with a non-const rvalue reference (`&&`) as its
parameter:

```c++
class string {
   private:
      int len;    // current number of characters
      char* data; // dynamic array of characters

   public:
      ...
      // move constructor: initialize the new string from s (stealing the value):
      string (string&& s)
         : len{s.len}, data{s.data} { // copy number of characters and pointer to memory
            s.data = nullptr;         // release the memory for the source value
            s.len = 0;                // and adjust number of characters accordingly
      }
      ...
};
```

A copy constructor would have worked like this:

![image-15.png](image-15.png)

We can call the move constructor for a string as follows:

```c++
std::string c = std::move(b); // init c with the value of b (no longer needing its value here)
```

The move constructor first copies both the members `len` and `data`, meaning that the new string gets ownership of the value of `b` (passed as `s`).
    
![image-16.png](image-16.png)
    
However, this is not enough, because the destructor of `b` would free the memory. Therefore, we also modify the source string to lose its ownership of the memory and bring it into a consistent state representing the empty string:

![image-17.png](image-17.png)

Note that the only guarantee is that `b` is subsequently in a valid but unspecified state.
    
### 1.3 Copying as a Fallback
    
If there is no optimized version of a function for move semantics, then the usual copying is used as a fallback.

<mark>So, if the `std::vector` class had no `void push_back(T&& elem);` to perform move semantics, then `void push_back(const T& elem);` would be used to perform copy semantics.</mark>

The rule is that for a temporary object or an object marked with `std::move()`, if available, a function declaring the parameter as an rvalue reference is preferred. However, if no such function exists, the usual copy semantics is used. That way, we ensure that the caller does not have to know whether an optimization exists.

For generic code, it is important that we can **always** mark an object with `std::move()` if we no longer need its value. The corresponding code compiles even if there is no move semantics support.

You can even mark objects of a fundamental data type such as `int` (or a pointer) with `std::move()`. The usual value semantics copying the value (or the address, in the case of a pointer) will still be used:

```c++
   std::vector<int> coll;
   int x{42};
   ...
   coll.push_back(std::move(x)); // OK, but copies x (std::move() has no effect)
```

### 1.4 Move Semantics for `const` Objects

Note that objects declared with `const` cannot be moved because any optimizing implementation requires that the passed argument can be modified. We cannot steal a value if we are not allowed to modify it.

The only valid function to call for `const` objects is the first overload of `push_back()` with the `const&` parameter:

```c++
std::vector<std::string> coll;
const std::string s{"data"};

coll.push_back(std::move(s)); // OK, calls push_back(const std::string&), VS 2019 shows a warning not to call move on constants.

coll
```

That means that a `std::move()` for const objects essentially has no effect. The `const` lvalue reference overload
serves as a fallback to handle this case.

### 1.4.1 const Return Values

The fact that `const` disables move semantics also has consequences for declaring return types. A `const` return value cannot be moved.

Therefore, since C++11, it is no longer good style to return by value with `const` (as some style guides have recommended in the past). For example:

```c++
const std::string getValue()
{
    return std::string{"data"};
}

std::vector<std::string> coll;

coll.push_back(getValue()); // copies (because the return value is const), no warning in VS 2019 - I'm surprised!

coll
```

When returning by value, do not declare the return value as a whole to be `const`. Use `const` only to declare parts of your return type (such as the object a returned reference or pointer refers to):

```c++
const std::string  getValue(); // BAD: disables move semantics for return values
const std::string& getRef();   // OK
const std::string* getPtr();   // OK
```

