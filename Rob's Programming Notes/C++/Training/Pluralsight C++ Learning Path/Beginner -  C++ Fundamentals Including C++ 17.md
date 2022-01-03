# Beginner: C++ Fundamentals Including C++ 17

**Created**: Sunday, April 08, 2018 10:00:28 PM -04:00
**Modified**: Friday, November 16, 2018 04:58:33 PM -05:00


https://app.pluralsight.com/library/courses/cplusplus-fundamentals-c17/table-of-contents

Duration: 5h 48m

4/15/2018
1:46 pm.to 2:18 pm
3:20 pm to 4:06

05/03/2018 (Flight home from Seattle on Alaska)

# Language Basics - Functions

1. Any function that is not a member of a class is called a free function.
2. `bool IsPrime(int const&amp; x)`
3. Mark functions as `const` unless you can't.
4. Never put `using namespace std;` in a header file.
5. ![Understanding Error Messages &#xA;compiler &#xA;Have you declared that function? &#xA;usually in a .h &#xA;making a promise &#xA;linker &#xA;Have you implemented that function? &#xA;usually in a .cpp &#xA;keeping the promise ](/Attachments/1-ddf376c8b5724bb9a6c34d275f7eb363.png)

# Language Basics - Operators

1. `if (3 == i)` is called a Yoda condition because it's backwards.
    1. She doesn't like this, but you can't get it wrong.
    2. You can also set Warning Level 4 and you don't need to use this format.

# 11/09/2019

1. Templates
    1. Templated Functions
        1. Algorithms that work on them.
        2. `T const& t1`
        3. Templates are often in header files.
    2. Templated Classes
        1. https://wandbox.org, online C++ compiler.
        2. Don't forget about https://godbolt.org/
        3. To initialize an empty string using C++ templated string class, use `string("")`.
    3. Template Specialization.
        1. This should not be your first choice, if you can help it.
        2. See her Accum example.
    4. Summary
        1. Most of the time, it is more important to be able to read templates than it is to write them.
        2. Watch her algorithms course after this one.
    5. Ternary operator is also known as the immediate operator.

# 11/10/2018
2. Indirection, i.e., pointers.
    1. References and Pointers
    2. `int* badPointer = nullptr`
    3. References in C++ can never be uninitialized.
3. `const`
    1. ![A way to commit to the compiler &#xA;you won't change something &#xA;When declaring a local variable &#xA;int const zero = e; &#xA;As a function parameter &#xA;int foo(int const i) &#xA;int something(Person const&amp;amp; p) &#xA;Modifier on a member function &#xA;int GetName() const; &#xA;Const correctness can be difficult ](/Attachments/1-ed79fc99255e4c06bb23a9c3af220e95.png)
        1. Know at the beginning how you want to treat a variable.
            1. Changing its const-ness after the fact can be difficult.
            2. You can find yourself wandering through code making changes all over if you try to change it later.
    2. Style: const refers to what it is after.
        1. `int const ci = 3;`
        2. This is the preferred choice in modern C++.
        3. **Do not write `const int ci = 3`.**
        4. Compiler doesn't care, but it's easier to read "const after" once you introduce references.
    3. If you see a message similar to `Expression must be a modifyable lvalue`, it is the compiler telling you that you're breaking the `const` rules.
    4. Reference
        1. `int I = 4`
        2. `int& ri = I`
        3. `ri = 5; // this is ok.`
        4. `int const & cri = i;`
        5. `cri = 6; // this is not ok`
        6. ![](/Attachments/1-a78cd864a91e4be8a3843664dbdfa27a.png)
        7. If you take the `const` off of the `int GetNumber() const { … }`, the above will fail.
    5. <mark style="background: #BBFABBA6;">If your function takes an int\& parameter, then you cannot pass a literal to it, e.g. 10.</mark>
        1. <mark style="background: #BBFABBA6;">You can fix this by making your function take int const\& x.</mark>
    6. Const with Indirection
        1. References cannot retarget.
        2. ![](/Attachments/1-45ced669d3de449e88f19cfaa91c7084.png)
        3. ![](/Attachments/1-9b0d02b9c29044f38c7fe681908adcbd.png)
        4. ![](/Attachments/1-e1170d7631fd4fc08e72fbc28887da24.png)
        5. <mark style="background: #BBFABBA6;">So, read right-to-left, e.g. crazy is a `const` pointer to a constant `int`.</mark>

# 11/12/2018
4. Memory Management
    1. The Free Store
        1. Variables are stored on the heap.
        2. Vs. local variables, which are stored on the stack.
        3. <mark style="background: #BBFABBA6;">Today you should refer to the heap as the free store.</mark>
        4. Use the new operator.
            1. Calls the constructor.
        5. Tear it down with the delete operator.
            1. Calls the destructor.
        6. <mark style="background: #BBFABBA6;">Modern C++ avoids "raw arrays", i.e., do not new and delete them.</mark>
            1. Use `vector`s or `array`s.
        7. <mark style="background: #BBFABBA6;">After you delete an object, set it to nullptr.</mark>
            1. It is safe to call delete on `nullptr`.
        8. ![](/Attachments/1-d6e13cf98b0a4b34b8d69f1e104dc9bd.png)
        9. ![](/Attachments/1-82a2ba503f3b481a903e6f05d3f98310.png)
        10. So if you have a pointer from the free store in your class, now you need to write at least five functions for your class.
        11. <mark style="background: #BBFABBA6;">She prefers the Rule of Zero: rely on a class from the library to do the memory management.</mark>
            1. Use Stack Semantics (aka Value Semantics)
        12. <mark style="background: #BBFABBA6;">A copy constructor only needs to make new copies of pointers in the class.</mark>
            1. You don't need to worry about things that are local variables.
        13. A templated class can have methods for all five required methods.
        14. Handle Copy and Move
            1. In older C++, you could mark the copy constructor as private so it couldn't be called.
                1. In modern C++, we can mark that constructor as deleted.
            2. You can implement deep copy.
                1. Or you can implement a shallow copy with a reference counter.
            3. An Operator Overload on \* always handles dereference operations.
                1. This makes it feel like a pointer.
                2. If the thing inside is an object, then you need to overload the -&gt; operator.
            4. C++11 added smart pointers.
                1. One that prevents copying, and
                2. One that provides shallow copying with reference counting.
    2. Standard Library Smart Pointers
        1. <mark style="background: #BBFABBA6;">Note that these structures all exist on the stack, but what they point to is in the free store, i.e., the heap.</mark>
        2. `unique_ptr`
            1. Very low overhead
            2. Noncopyable (use `std::move` to move it around at all)
        3. `shared_ptr`
            1. This can be copied.
            2. Uses reference counting.
            3. Not as useful as you might think.
        4. `weak_ptr`
            1. Lets you peek at the `shared_ptr` without bumping the reference count.
            2. Use with caution.
                1. Including for testing.
            3. Make sure that the resource still exists.
        5. `std::shared_ptr<Resource> pResource;`
            1. Test it before you use it to make sure that the resource still exists.
                1. e.g. `return pResource ? pResource->GetName() : "";`.
                2. <mark style="background: #BBFABBA6;">Shared and unique pointers will return `false` if they don't point to anything and `true` if they do.</mark>
            2. In the previous version of the code that used raw pointers, i.e., `Resource* pResource`, make sure that `GetResourceName()` returns `""` instead of `nullptr` or your code could have blown up.
                1. **Continuing on 11/16/2018**
        6. `#include <memory>;` to use these.
        7. They have default constructors, so no need to initialize shared/unique pointers to `nullptr`.
        8. Using them may also eliminate your need for a destructor.
            1. <mark style="background: #BBFABBA6;">Confusing to have a destructor b/c then it looks like you're not completely following the rule or three or the rule of five.</mark>
        9. Instead of calling delete on unique/shared pointers, you call `reset`.
            1. <mark style="background: #FFF3A3A6;">This may only be on shared pointers, not sure.</mark>
        10. You don't call new to create an instance of a shared pointer.  You call `std::make_shared<Resource>()`.
            1. There is also `std::make_unique` when using unique pointers.
            2. <mark style="background: #BBFABBA6;">`make_shared` gets you the best performance.</mark>
5. Indirection and Inheritance
    1. References and Inheritance
        1. Base class reference can actually refer to a derived class instance.
        2. Respects the "is a" relationship.
        3. Vital to Liskov substitutability.
        4. Which code runs, the base class or the derived class?
        5. In C++, the answer is "it depends".
            1. <mark style="background: #BBFABBA6;">If the function has been marked virtual, then the derived method runs.</mark>
            2. This is known as polymorphism.
            3. <mark style="background: #BBFABBA6;">If the function is non-virtual, then the base class method runs.</mark>
        6. There is a cost to calling virtual functions.
            1. Memory cost for virtual table.
            2. Performance cost of the lookup.
    2. Pointers and Inheritance
        1. Works the same as references.
    3. Smart Pointers and Inheritance
        1. Exactly the same behavior.
    4. You can mark private member variables as protected to let derived classes access them.
        1. **She doesn't like it**.
        2. To her, **protected is like a to-do list**.
        3. <mark style="background: #BBFABBA6;">Completely encapsulate your base class.</mark>
        4. So, call `Person::GetName()` and you don't need access to `firstname` and `lastname` from the base class.
    5. <mark style="background: #BBFABBA6;">Most of the time, you want to mark functions as virtual so you get the behavior of the derived class.</mark>
    6. If you have a destructor in a derived class but you create a pointer to a base class, the derived destructor will never get called.
        1. <mark style="background: #BBFABBA6;">As soon as you have one virtual function in your derived class, ALWAYS make your derived class' destructor virtual.</mark>
        2. **Otherwise you are setting yourself up for memory leaks in the derived destructor that never gets called.**
    7. Slicing
        1. Happens when you copy objects.
        2. <mark style="background: #BBFABBA6;">If you copy a derived object into a base object, there's nowhere for the extra member variables to go, so they just fall away.</mark>
        3. You cannot copy a base object into a derived object.
        4. When you pass objects by value, you are making copies.