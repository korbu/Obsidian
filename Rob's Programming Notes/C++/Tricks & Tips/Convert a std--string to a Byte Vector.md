# Convert a std::string to a Byte Vector

**Created**: Monday, June 17, 2019 01:01:50 PM -04:00
**Modified**: Monday, June 17, 2019 01:03:48 PM -04:00

```c++
const std::string TEST_STRING = "This is my test string";
std::vector<BYTE> stringAsByteVector;
stringAsByteVector.assign(TEST_STRING.begin(), TEST_STRING.end());
```

