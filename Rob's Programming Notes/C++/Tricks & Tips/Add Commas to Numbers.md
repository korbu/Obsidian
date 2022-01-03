# Add Commas to Numbers

**Created**: Thursday, August 09, 2018 11:42:24 AM -04:00
**Modified**: Thursday, August 09, 2018 11:46:05 AM -04:00

```c++
#include <iomanip>
#include <locale>
#include <iostream>
#include <sstream>

template<class T>
std::string FormatWithCommas(T value)
{
    static std::locale loc("");
    
    std::stringstream ss;
    ss.imbue(loc);
    ss << std::fixed << value;
    
    return ss.str();
}

void main()
{
    std::cout << FormatWithCommas(123456789) << std::endl;
    std::cout << FormatWithCommas(-123456789) << std::endl;
}
```

https://stackoverflow.com/questions/7276826/c-format-number-with-commas