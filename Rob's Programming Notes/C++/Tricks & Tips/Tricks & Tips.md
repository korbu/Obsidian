# Tricks & Tips

**Created**: Thursday, August 09, 2018 11:44:20 AM -04:00
**Modified**: Monday, July 29, 2019 08:53:23 PM -04:00


# A Tour of C++: Chapter 4

1. Functions defined in a class are inlined by default.
2. A const member function can be invoked for both const and non-const objects.
3. But a non-const member function can only be invoked for non-const objects.
4. `std::initializer_list()` to initialize within a constructor.
5. Explicit type conversions are often called casts to remind you that they are used to prop up something broken.  They are best avoided.
6. reinterpret\_cast treats an object as simply a sequence of bytes.
7. An abstract type is a type that completely insulates a user from implementation details. To do that, we decouple the interface from the representation and give up genuine local variables.
8. The word virtual means "may be redefined later in a class derived from this one."
9. The curious =0 syntax says the function is pure virtual; that is, some class derived from Container (the abstract class) must define the function.
10. A class with a pure virtual function is called an abstract class.
11. As is common for abstract classes, Container does not have a constructor.
    1. After all, it does not have any data to initialize.
12. On the other hand, Container does have a destructor and that destructor is virtual, so that classes derived from Container can provide implementations.
    1. Again, that is common for abstract classes because they tend to be manipulated through references or pointers, and someone destroying a Container through a pointer has no idea what resources are owned by its implementation.
13. I used the explicit override to make clear what’s intended. The use of override is optional, but being explicit allows the compiler to catch mistakes, such as misspellings of function names or slight differences between the type of a virtual function and its intended overrider.
14. Note that the member destructor (`˜Vector()`) is implicitly invoked by its class’s destructor (`˜Vector_container()`), i.e., the parent's destructor is implicitly invoked by its child's destructor.
15. Performance of list subscripting is atrocious compared to vector subscripting.
16. The usual implementation technique is for the compiler to convert the name of a virtual function into an index into a table of pointers to functions. That table is usually called the virtual function table or simply the vtbl.