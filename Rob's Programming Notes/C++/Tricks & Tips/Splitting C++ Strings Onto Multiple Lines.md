# Splitting C++ Strings Onto Multiple Lines

**Created**: Saturday, October 13, 2018 09:45:16 AM -04:00
**Modified**: Saturday, October 13, 2018 09:46:09 AM -04:00


Don't put anything between the strings. Part of the C++ lexing stage is to combine adjacent string literals (even over newlines and comments) into a single literal.

```c++
std::string = "This is a single "
"string in C++";
```
