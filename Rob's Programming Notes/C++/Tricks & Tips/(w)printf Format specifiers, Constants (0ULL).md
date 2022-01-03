# (w)printf Format specifiers, Constants (0ULL)

**Created**: Tuesday, August 07, 2018 03:48:14 PM -04:00
**Modified**: Tuesday, April 09, 2019 12:27:50 PM -04:00

https://docs.microsoft.com/en-us/cpp/c-runtime-library/format-specification-syntax-printf-and-wprintf-functions

| **Type character** | **Argument** | **Output format** |
| --- | --- | --- |
| c | Character | When used with `printf` functions, specifies a single-byte character; when used with `wprintf` functions, specifies a wide character. |
| C | Character | When used with `printf` functions, specifies a wide character; when used with `wprintf` functions, specifies a single-byte character. |
| d | Integer | Signed decimal integer. |
| i | Integer | Signed decimal integer. |
| o | Integer | Unsigned octal integer. |
| u | Integer | Unsigned decimal integer. |
| x | Integer | Unsigned hexadecimal integer; uses &quot;abcdef.&quot; |
| X | Integer | Unsigned hexadecimal integer; uses &quot;ABCDEF.&quot; |
| e | Floating-point | Signed value that has the form [-]*d.dddd*e&#177;*dd*[*d*] where *d* is one decimal digit, *dddd* is one or more decimal digits depending on the specified precision, or six by default, and *dd*[*d*] is two or three decimal digits depending on the [output format](https://docs.microsoft.com/en-us/cpp/c-runtime-library/set-output-format) and size of the exponent. |
| E | Floating-point | Identical to the e format except that E rather than e introduces the exponent. |
| f | Floating-point | Signed value that has the form [-]*dddd*.*dddd*, where *dddd* is one or more decimal digits. The number of digits before the decimal point depends on the magnitude of the number, and the number of digits after the decimal point depends on the requested precision, or six by default. |
| F | Floating-point | Identical to the f format except that infinity and nan output is capitalized. |
| g | Floating-point | Signed values are displayed in f or e format, whichever is more compact for the given value and precision. The e format is used only when the exponent of the value is less than -4 or greater than or equal to the *precision* argument. Trailing zeros are truncated, and the decimal point appears only if one or more digits follow it. |
| G | Floating-point | Identical to the g format, except that E, rather than e, introduces the exponent (where appropriate). |
| a | Floating-point | Signed hexadecimal double-precision floating-point value that has the form [-]0x*h.hhhh*p&#177;*dd*, where *h.hhhh* are the hex digits (using lower case letters) of the mantissa, and *dd* are one or more digits for the exponent. The precision specifies the number of digits after the point. |
| A | Floating-point | Signed hexadecimal double-precision floating-point value that has the form [-]0X*h.hhhh*P&#177;*dd*, where *h.hhhh* are the hex digits (using capital letters) of the mantissa, and *dd* are one or more digits for the exponent. The precision specifies the number of digits after the point. |
| n | Pointer to integer | Number of characters that are successfully written so far to the stream or buffer. This value is stored in the integer whose address is given as the argument. The size of the integer pointed to can be controlled by an argument size specification prefix. The n specifier is disabled by default; for information see the important security note. |
| p | Pointer type | Displays the argument as an address in hexadecimal digits. |
| s | String | When used with `printf` functions, specifies a single-byte or multi-byte character string; when used with `wprintf` functions, specifies a wide-character string. Characters are displayed up to the first null character or until the *precision* value is reached. |
| S | String | When used with `printf` functions, specifies a wide-character string; when used with `wprintf` functions, specifies a single-byte or multi-byte character string. Characters are displayed up to the first null character or until the *precision* value is reached. |
| Z | `ANSI_STRING` or `UNICODE_STRING` structure | When the address of an [ANSI_STRING](http://msdn.microsoft.com/library/windows/hardware/ff540605.aspx) or [UNICODE_STRING](http://msdn.microsoft.com/library/windows/hardware/ff564879.aspx) structure is passed as the argument, displays the string contained in the buffer pointed to by the `Buffer` field of the structure. Use a *size* modifier prefix of w to specify a `UNICODE_STRING` argument—for example, `%wZ`. The `Length` field of the structure must be set to the length, in bytes, of the string. The `MaximumLength` field of the structure must be set to the length, in bytes, of the buffer.<br /><br /><br />Typically, the Z type character is used only in driver debugging functions that use a conversion specification, such as `dbgPrint` and `kdPrint`. |

<mark style="background: #FFF3A3A6;">%lld???</mark>

From &lt;https://docs.microsoft.com/en-us/cpp/c-runtime-library/format-specification-syntax-printf-and-wprintf-functions&gt;

# C++ Constants

## Integers

```c++
0    // normal number is interpreted as int
0L   // ending with 'L' makes it a long
0LL  // ending with 'LL' makes it long long
0UL  // unsigned long
0ULL // unsigned long long
0x   // prefix that makes it a hexadecimal literal.
```

## Floating Point
```c++
0.0  // decimal point makes it a double
0.0f // 'f' makes it a float
1.0L // of type 'long double'
```


## Strings and Characters
```c++
'A'   // of type 'char'
L'A'   // of type 'wchar\_t'
u'A'   // of type 'char16\_t' (C++0x only)
U'A'   // of type 'char32\_t' (C++0x only)
```


From https://stackoverflow.com/questions/7036056/what-do-0ll-or-0x0ul-mean.