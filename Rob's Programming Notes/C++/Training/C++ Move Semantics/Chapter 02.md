# C++ Move Semantics

by Nicolai M. Josuttis

## Chapter 2: Core Features of Move Semantics

## 2.1 Rvalue References

## 2.1.1 Rvalue References in Detail

rvalue references refer to an existing object that has to be passed as an initial value. However, according to their semantic meaning, rvalue references can refer only to:
1. a temporary object that does not have a name, or
2. to an object marked with `std::move()`:

```c++
#include <string>

std::string returnStringByValue()
{
    return "data";
}

std::string s{"hello"};

// std::string&& r1{s};                  // ERROR
std::string&& r2{std::move(s)};          // OK, fixes the above line
std::string&& r3{returnStringByValue()}; // OK, extends lifetime of return value

"r2 = " + r2 + ", r3 = " + r3
```

References extend the lifetime of the return value until the end of the lifetime of the reference.

The syntax used to initialize the reference is irrelevant. You can use:

1. the equal sign,
2. braces, or
3. parentheses

```c++
std::string s{"hello"};

std::string&& r1 = std::move(s); //OK, rvalue reference to s
std::string&& r2{std::move(s)};  //OK, rvalue reference to s
std::string&& r3(std::move(s));  //OK, rvalue reference to s
```

All these references have the semantics of "we can steal/modify the object we refer to, provided the state of the object remains a valid state." Technically, these semantics are not checked by compilers, so we can modify an rvalue reference as we can do with any non-const object of the type.

We might also decide not to modify the value. That is, if you have an rvalue reference to an object, the object might receive a different value (which might or might not be the value of a default-constructed object) or it might keep its value.

If compilers automatically detect that a value is used from an object that is at the end of its lifetime, they will automatically switch to move semantics. This is the case when:

1. We pass the value of a temporary object that will automatically be destroyed after the statement.
2. We pass a non-const object marked with `std::move()`.

## 2.1.2 Rvalue References as Parameters

```c++
#include <string>

// takes only objects where we no longer need the value
void foo(std::string&& rv) {
}

std::string returnStringByValue() {
    return std::string{"data"};
}

std::string s{"hello"};

// foo(s);                     // ERROR
foo(std::move(s));          // OK, value of s might change
foo(returnStringByValue()); // OK
```

You can use a named object after passing it with `std::move()` but usually you should not. The recommended programming style is to no longer use an object after a `std::move()`:

```c++
#include <string>

std::string s{"hello"};

s
```

## 2.3 Moved-From Objects