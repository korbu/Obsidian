# C++ at the end of 2021
**Created**: Friday, December 31, 2021 11:57:27 AM -05:00

[C++ Stories](https://www.cppstories.com/)

Stay up-to-date with Modern C++

Last Update: 31 December 2021

# C++ at the end of 2021

![](https://www.cppstories.com/2021/images/cpp2021.png)

I’m happy to present the 10th edition of “C++ at the end”! See what happened this year in the C++ World!

New features, plans for the language, updated tools and compilers, conferences, books, and more!

What was the most important event this year? The pandemic? C++20 adoption? Ongoing work for C++23 or something else?

Let’s have a look.

**Reports from previous years:** [2020](https://www.cppstories.com/2020/12/cpp-status-2020/), [2019](https://www.cppstories.com/2019/12/cpp-status-2019.html/), [2018](https://www.cppstories.com/2018/12/c-at-end-of-2018.html), [2017](https://www.cppstories.com/2017/12/cpp-status-2017.html), [2016](https://www.cppstories.com/2016/12/c-status-at-end-of-2016.html), [2015](https://www.cppstories.com/2015/12/c-status-at-end-of-2015.html), [2014](https://www.cppstories.com/2014/12/c-status-at-end-of-2014.html), [2013](https://www.cppstories.com/2013/12/c-status-at-end-of-2013/), [2012](https://www.cppstories.com/2012/12/c-at-end-of-2012.html).

The following companies support this year’s report:

[![](https://www.cppstories.com/2021/images/valogo16.png)](https://www.wholetomato.com/?utm_source=Bartek&utm_medium=Leads%20Acquisition&utm_content=Article-Dec21&utm_campaign=Article-Dec21) [![](https://www.cppstories.com/2021/images/embarcadero32.png)](https://www.embarcadero.com/?utm_source=Bartek&utm_medium=Leads%20Acquisition&utm_content=Article-Dec21&utm_campaign=Article-Dec21)  [![](https://www.cppstories.com/2021/images/sonarsource32.png)](https://www.sonarsource.com/?utm_medium=paid&utm_source=cppstories&utm_campaign=cpp&utm_content=eoynewsletter)  [![](https://www.cppstories.com/2021/images/jetbrains48.png)](https://www.jetbrains.com/) [![](https://www.cppstories.com/2021/images/pvs50.png)](https://pvs-studio.com/static_analyzer)

**Disclaimer:** the view presented here is mine and does not represent the opinion of the ISO C++ committee, companies I work for, or sponsors.

## A Brief Introduction

2021 was the full pandemic year, and we all seem to be tired, frightened, bored, or even divided (in various proportions). It looks like we have already accepted that the situation won’t change anytime soon. Focusing on programming, we can say that we’re lucky to adapt so fast to new life and workstyle in most cases. For many, working from home might be better than in the office, but ideally, having a mix is probably preferred.

Regarding C++, I see the following major trends and topics in 2021:

-   C++20 adoption,
-   C++23 ongoing, but seemed to be slowed by pandemic,
-   Better tools.

Read on to get the complete picture.

## Timeline

The below table helps to see the main events:

| Date | Event |
| --- | --- |
| February 22nd | Virtual plenary meeting, ISO C++, WG21 |
| March 9 - 14 | Accu 2021 |
| March 11th | PVS-Studio 7.12 |
| April 7/8 | CLion 2021.1 & ReSharper C++ 2021.1 |
| April 14th | Clang 12.0 |
| May 2–7 | C++ Now |
| June 7th | Virtual plenary meeting, ISO C++, WG21 |
| June 19th | Italian C++ Conference |
| July 28th | CLion 2021.2 |
| July 14th | HPX V17.0 Released |
| July 28th | GCC 11.2 |
| August 3rd | ReSharper C++ 2021.2 |
| August 10th | Visual studio 2019 16.11.0 |
| August 11th | Boost 1.77 |
| September 10th | C++ Builder 11.0 Alexandria |
| October 4th | Clang 13.0 |
| October 4th | Virtual plenary meeting, ISO C++, WG21 |
| October 25 - 29 | CppCon 2021 |
| November 8th | Visual Studio 2022 generally available! |
| November 10 - 12 | Meeting C++ 2021 |
| November 15 - 18 | C++ Russia |
| December 1st | CLion 2021.3 |
| December 8th | ReSharper C++ 2021.3 |
| December 10th | PVS-Studio 7.16 |

## Compiler Support for C++17

It’s four years after C++17 was published, and this year we can say that all major compilers support the language features!

The only tricky thing is Parallelism - parallel algorithms. Clang still misses it, while GCC leverages Intel TBB as the backed infrastructure.

This year there was also good progress with floating-point support for low-level conversion routines - `from_chars` and `to_chars`. While integers have worked since early versions of GCC and Clang, the floats and doubles support happens only in version GCC 11 and Clang 14. The MSVC compiler implemented both numerical categories a long time ago.

You can find full data at [C++17 compiler support - cppreference.com](https://en.cppreference.com/w/cpp/compiler_support#cpp17)

Additionally since GCC 11: [GCC 11 Now Defaults To C++17 Dialect By Default - Phoronix](https://www.phoronix.com/scan.php?page=news_item&px=GCC-11-Cpp-17-Default)

and if you want to learn all features from C++17, here’s my oveview: [C++ 17 Features - C++ Stories](https://www.cppstories.com/2017/01/cpp17features/)

## Compiler Support For C++20

On the other hand, it’s only one year after C++20 was standardized, and major compilers are very close to announcing full conformance!

Here are some of the best features added to the Standard:

-   Modules
-   Coroutines
-   Concepts and Concepts in the Standard Library
-   Ranges
-   operator `<=>` and its use in the Standard Library, simplified operator rewriting rules
-   Text formatting - `std::format`
-   Calendar and timezones
-   `jthread`, semaphores, more atomics, barriers, and more concurrency stuff
-   `consteval` and `constinit`
-   `constexpr` algorithms, vector, string, memory allocations
-   `std::span`
-   and more!

And here’s the table with compiler notes for language features:

| Compiler | Notes |
| --- | --- |
| GCC 11 | Only Modules are in the “partial” state |
| Clang 12 | partial for lambda features, NTTP, coroutines, modules, consteval, missing: Make `typename` more optional, conditionally Trivial Special Member Functions, CTAD improvements |
| MSVC 16.9 | Full support! |

While Clang was usually the fastest to implement various improvements, it looks like it slowed down, and other compilers (mostly MSVC) are taking its position.

Regarding library features:

| Compiler | Notes |
| --- | --- |
| GCC libstdc++ | missing `make_shared` for arrays, `make_unique_for_overwrite`, **text formatting**, small atomic bits |
| Clang libc++ | missing `make_shared` for arrays, FP atomics, `osyncstream`, atomics bits, `make_unique_for_overwrite`, Standard library header units, `std::execution::unseq`, `jthread`, constexpr `string` and `vector`, partial text formatting, |
| MSVC STL | Full support as of MSVC 16.9, 17.0! |

You can track the status [@cppreference - C++20 support](https://en.cppreference.com/w/cpp/compiler_support#cpp20).

If you want to learn all features, you can see this great and super popular blog post by Oleksandr Koval:

[All C++20 core language features with examples](https://oleksandrkvl.github.io/2021/04/02/cpp-20-overview.html)

This year at C++ Stories I also covered a lot of features from the new standard:

-   [Designated Initializers in C++20 - C++ Stories](https://www.cppstories.com/2021/designated-init-cpp20/)
-   [C++20: Heterogeneous Lookup in (Un)ordered Containers - C++ Stories](https://www.cppstories.com/2021/heterogeneous-access-cpp20/)
-   [C++20 Oxymoron: constexpr virtual - C++ Stories](https://www.cppstories.com/2021/constexpr-virtual/)
-   [constexpr vector and string in C++20 and One Big Limitation - C++ Stories](https://www.cppstories.com/2021/constexpr-vecstr-cpp20/)
-   [Empty Base Class Optimisation, no_unique_address and unique_ptr - C++ Stories](https://www.cppstories.com/2021/no-unique-address/)
-   [Predefined C++20 Concepts: Callables - C++ Stories](https://www.cppstories.com/2021/concepts-callables/)
-   [C++20 Concepts - a Quick Introduction - C++ Stories](https://www.cppstories.com/2021/concepts-intro/)
-   [Increased Complexity of C++20 Range Algorithms Declarations - Is It Worth? - C++ Stories](https://www.cppstories.com/2020/10/complex-ranges-algorithms.html/)

Here’s the tag with more than 45 articles (and growing) at the blog: [Cpp20 - C++ Stories](https://www.cppstories.com/tags/cpp20/).

And have a look at modernescpp where Rainer Grimm covered probably all of the features in his long article series:

-   [C++20 Modules: Private Module Fragment and Header Units - ModernesCpp.com](https://www.modernescpp.com/index.php/c-20-modules-private-module-fragment-and-header-units)
-   [Latches in C++20 - ModernesCpp.com](https://www.modernescpp.com/index.php/latches-in-c-20)
-   [Barriers and Atomic Smart Pointers in C++20 - ModernesCpp.com](https://www.modernescpp.com/index.php/barriers-in-c-20)
-   [Semaphores in C++20 - ModernesCpp.com](https://www.modernescpp.com/index.php/semaphores-in-c-20)
-   [Bit Manipulation with C++20 - ModernesCpp.com](https://www.modernescpp.com/index.php/bit-manipulation-with-c-20)
-   [Calendar and Time-Zones in C++20: Time-Zones - ModernesCpp.com](https://www.modernescpp.com/index.php/calendar-and-time-zone-in-c-20-time-zones)
-   [std::format in C++20 - ModernesCpp.com](https://www.modernescpp.com/index.php/std-format-in-c-20)

Additionally, you can also check out Jason Turner’s C++ Weekly with most C++20 features covered:

-   [C++ Weekly C++20 Playlist - YouTube](https://www.youtube.com/playlist?list=PLs3KjaCtOwSYdpfm74DYyd1kOXEhCd1Rv)
-   [C++ Weekly - Ep 194 - From SFINAE To Concepts With C++20 - YouTube](https://www.youtube.com/watch?v=dR64GQb4AGo&list=PLs3KjaCtOwSYdpfm74DYyd1kOXEhCd1Rv&index=20)
-   [C++ Weekly - Ep 261 - C++20’s New consteval Keyword - YouTube](https://www.youtube.com/watch?v=b22cKntJslU&list=PLs3KjaCtOwSYdpfm74DYyd1kOXEhCd1Rv&index=40)

## The C++23 Status

If you cannot cope with new features in C++20… don’t worry; C++23 is just around the corner with cool new stuff :)

What’s more, some compilers already support a lot of features!

While it’s the end of 2021, we’re just two months away from marking the standard “feature freeze,” and no new features will be added.

Today, we know (and that was the plan) that C++23 will be much smaller than C++20, maybe even smaller than C++17. This new Standard will “complement” and finalize prominent features added in C++20.

Some features and their current support (including language and library elements):

| Feature | GCC | Clang | MSVC |
| --- | --- | --- | --- |
| Make `()` more optional for lambdas | 11.0 | 13.0 | x |
| `if consteval` | 12.0 | 14.0 | x |
| Deducing `this` | x | x | x |
| Multidimensional subscript operator | 12.0 | x | x |
| Stacktrace library | x | x | x |
| `std::is_scoped_enum` | 11.0 | 12.0 | VS 2022 17.0 |
| `contains()` for strings and string views | 11.0 | 12.0 | VS 2022 17.0 |
| `constexpr` for `std::optional` and `std::variant` | 12.0 | 13.0 | VS 2022 17.1 |

Later this year, we could hear some updates from the members of the ISO Committee:

-   [C++23 ISO Progress](https://cppcast.com/cpp23-iso-progress/) with Bryce Adelstein Lelbach
-   [C++23: Near The Finish Line](https://www.reddit.com/r/cpp/comments/qug17i/c23_near_the_finish_line/) at Reddit

Some features that will probably land in C++23:

-   `std::execution`, [P2300](https://wg21.link/P2300)
-   A Plan for C++23 Ranges, [P2214](https://wg21.link/P2214) (split into several separate papers)
-   `std::generator`: Synchronous Coroutine Generator for Ranges, [P2168](https://wg21.link/P2168)
-   `std::lazy`, [P1056](https://wg21.link/P1056) - lazy coroutine (coroutine task) type
-   Formatted Output - `std::print`, [P2093](https://wg21.link/P2093)
-   `std::mdspan`, [P0009](https://wg21.link/P0009)
-   Mixed Comparisons For Smart Pointers, [P2249](https://wg21.link/P2249)

Networking has no consensus - TS is probably not worth putting into the Standard with its current state. Networking TS is also based on the ASIO model, and that can conflict with other features related to async. Do we need to have a single model for async processing? And last year, it appeared that this would not be going to work.

## ISO C++ Online Meetings

While all face-to-face gatherings are canceled, the ISO committee meets regularly on online meetings.

All SG groups work on their tasks and set of features. For example, in 2020, there were around 200 meetings in total. The number might be similar for 2021.

The committee has to vote on the features and merge them in the current draft from time to time. This usually happens in physical meetings, but there are online plenary sessions now. This year we had three of them:

-   February 22nd
-   June 7th
-   October 4th

You can get a grasp of the current “virtual” ISO process in this cool podcast with Bryce Adelstein Lelbach [C++23 ISO Progress @CppCast](https://cppcast.com/cpp23-iso-progress/).

And here are the reports written by Herb Sutter from two of those plenary meetings:

-   [Trip report: Summer 2021 ISO C++ standards meeting (virtual) – Sutter’s Mill](https://herbsutter.com/2021/06/09/trip-report-summer-2021-iso-c-standards-meeting-virtual/)
-   [Trip report: Winter 2021 ISO C++ standards meeting (virtual) – Sutter’s Mill](https://herbsutter.com/2021/02/22/trip-report-winter-2021-iso-c-standards-meeting-virtual/)

And here’s the current status:

[Current Status : Standard C++](https://isocpp.org/std/status)

Mailings available in a nice table from isocpp.org:

-   [2021-12 Mailing Available](https://isocpp.org//blog/2021/12/2021-12-mailing-available)
-   [2021-11 Mailing Available](https://isocpp.org/blog/2021/11/2021-11-mailing-available)
-   [2021-09 Mailing Available](https://isocpp.org/blog/2021/09/2021-09-mailing)
-   [2021-08 Mailing Available](https://isocpp.org/blog/2021/09/2021-08-mailing-available)
-   [2021-07 Mailing Available](https://isocpp.org/blog/2021/07/2021-07-mailing-available)
-   [2021-06 Mailing Available](https://isocpp.org/blog/2021/06/2021-06-mailing-available)
-   [2021-05 Mailing Available](https://isocpp.org/blog/2021/05/2021-05-mailing-available)
-   [2021-04 Mailing Available](https://isocpp.org/blog/2021/04/2021-04-mailing-available)
-   [2021-03 Mailing Available](https://isocpp.org/blog/2021/03/2021-03-mailing-available)
-   [2021-02 Mailing Available](https://isocpp.org/blog/2021/02/2021-02-mailing-available)
-   [2021-01 Mailing available](https://isocpp.org/blog/2021/01/2021-01-mailing-available)

## Compilers

Compiler vendors impress me with the speed of implementing new features and adding various improvements to the build stack.

### Visual Studio

This year, Microsoft released their official stable version of the new IDE: Visual Studio 2022 (current version 17.0)

See the release notes: [What’s new in Visual Studio 2022 | Microsoft Docs](https://docs.microsoft.com/en-us/visualstudio/ide/whats-new-visual-studio-2022?view=vs-2022)

And the presentation by Scott Hanselman:

[Welcome to Visual Studio 2022](https://aka.ms/vs/yt/keynote)

![](https://www.cppstories.com/2021/images/welcome_vs22.webp)

Some of the most significant changes:

-   It is the first version to run as a 64-bit process! This change allows the Visual Studio process to access more than 4GB of memory which helps in large projects.
-   Hot Reload for C# and native C++ apps! It’s based on Edit & Continue.

A cool presentation about best feature for C++:

[What’s New in Visual Studio: 64-bit IDE, C++20, WSL 2, & More - Marian Luparu & Sy Brand - CppCon 21 @YouTube](https://www.youtube.com/watch?v=GIdIqfeePHQ)

Some MSVC news and blogs:

-   [Speed up your .NET and C++ development with Hot Reload in Visual Studio 2022](https://devblogs.microsoft.com/visualstudio/speed-up-your-dotnet-and-cplusplus-development-with-hot-reload-in-visual-studio-2022/)
-   [MSVC C++20 and the /std:c++20 Switch - C++ Team Blog](https://devblogs.microsoft.com/cppblog/msvc-cpp20-and-the-std-cpp20-switch/)
-   [Static Analysis Fixes in Visual Studio 2019 version 16.11](https://devblogs.microsoft.com/cppblog/static%e2%80%afanalysis-fixes-in-visual-studio-2019-version-16-11/)
-   [Moving a project to C++ named Modules](https://devblogs.microsoft.com/cppblog/moving-a-project-to-cpp-named-modules/)
-   [Edit Your C++ Code while Debugging with Hot Reload in Visual Studio 2022](https://devblogs.microsoft.com/cppblog/edit-your-c-code-while-debugging-with-hot-reload-in-visual-studio-2022/)
-   [2x-3x Performance Improvements for Debug Builds](https://devblogs.microsoft.com/cppblog/2x-3x-performance-improvements-for-debug-builds/)
-   [Address Sanitizer for MSVC Now Generally Available](https://devblogs.microsoft.com/cppblog/address-sanitizer-for-msvc-now-generally-available/)

And here’s a documentation page about the conformance with C++ Standards (including C++20): [Microsoft C++ language conformance table](https://docs.microsoft.com/en-us/cpp/overview/visual-cpp-language-conformance?view=vs-2019)

Additionally, you can track the progress of the Standard Library implementation at Github: [Changelog · Microsoft/STL Wiki](https://github.com/microsoft/STL/wiki/Changelog).

### GCC

Current stable version GCC 11.2 from July 28 [GCC 11 Release Series](https://gcc.gnu.org/gcc-11/).

You can also see the preview of the upcoming GCC 12: [GCC 12 Release Series — Changes, New Features, and Fixes - GNU Project](https://gcc.gnu.org/gcc-12/changes.html).

Among various new language features added into the latest versions of GCC, the big news is a new linker, called “mold”. [rui314/mold: mold: A Modern Linker](https://github.com/rui314/mold) [Mold (linker) 1.0 released [LWN.net]](https://lwn.net/Articles/878847/)

The new linker offers dramatic speedup for the linking phase. For example, in one benchmark, compiling Chrome 96 goes down from 53 seconds (Gold linker) into just **2 seconds**!

It will be added into GCC 12: [GCC 12 Adds Support For Using The Mold Linker - Phoronix](https://www.phoronix.com/scan.php?page=news_item&px=GCC-12-Mold-Linker).

Language and the Library support notes:

-   [Current C++ Support in GCC](https://gcc.gnu.org/projects/cxx-status.html)
-   [Libstdc++ Status](https://gcc.gnu.org/onlinedocs/libstdc++/manual/status.html)
-   [Libstdc++ C++ 2020 Status](https://gcc.gnu.org/onlinedocs/libstdc++/manual/status.html#status.iso.2020)

### Clang

Current stable version: 13.0.0 from October 4, [Release Notes — Clang 13 documentation](https://releases.llvm.org/13.0.0/tools/clang/docs/ReleaseNotes.html).

And also, you can preview Clang 14: [Clang 14.0.0 (In-Progress) Release Notes](https://clang.llvm.org/docs/ReleaseNotes.html).

-   [Current C++ Support in Clang](http://clang.llvm.org/cxx_status.html)
-   [libc++ C++20 Status — libc++ 12.0 documentation](https://libcxx.llvm.org/docs/Cxx2aStatus.html)
-   [libc++ C++2b Status — libc++ 12.0 documentation](https://libcxx.llvm.org/docs/Cxx2bStatus.html)

### C++ Builder

The current version is C++Builder 11 Alexandria, released on the 10th of September along with RAD Studio.

See [the release notes](https://docwiki.embarcadero.com/RADStudio/Alexandria/en/What%27s_New?utm_source=Bartek&utm_medium=Leads%20Acquisition&utm_content=Article-Dec21&utm_campaign=Article-Dec21).

![Rad Studio Alexandria](https://www.cppstories.com/2021/images/radstudio.webp)

The IDE uses a modified Clang Compiler (version 5.5, see [the compiler notes](https://docwiki.embarcadero.com/RADStudio/Alexandria/en/Clang-enhanced_C%2B%2B_Compilers?utm_source=Bartek&utm_medium=Leads%20Acquisition&utm_content=Article-Dec21&utm_campaign=Article-Dec21)), supports C++17. The Dinkumware C++17 STL implementation works with both Win32 and Win64 apps. C++Builder is a full-featured IDE for building iOS, Android, Windows, and macOS apps from a single C++ codebase.

You can also check the Community version: [C++Builder: Community Edition - Embarcadero](https://www.embarcadero.com/products/cbuilder/starter?utm_source=Bartek&utm_medium=Leads%20Acquisition&utm_content=Article-Dec21&utm_campaign=Article-Dec21).

Interestingly, Embarcadero supported Dev C++, and they managed to release a new (and free) version of this excellent and small IDE! Here’s the Github link: [Embarcadero/Dev-Cpp: A fast, portable, simple, and free C/C++ IDE](https://github.com/Embarcadero/Dev-Cpp/)

## IDE and Productivity

Here’s a nice overview of the whole C++ Ecosystem: [C++ Ecosystem: Compilers, IDEs, Tools, Testing and More - C++ Stories](https://www.cppstories.com/2019/10/cppecosystem/)

And below, you can find a list of their updates in 2021:

### Visual Assist

Visual Assist is a powerful addition to any of Visual Studio versions; it improves almost every aspect of VS IDE.

The latest version is from November 2021 - see the latest [Release notes](https://www.wholetomato.com/features/whats-new#2440?utm_source=Bartek&utm_medium=Leads%20Acquisition&utm_content=Article-Dec21&utm_campaign=Article-Dec21)

[![](https://www.cppstories.com/2021/images/valogo.png)](https://www.wholetomato.com/features?utm_source=Bartek&utm_medium=Leads%20Acquisition&utm_content=Article-Dec21&utm_campaign=Article-Dec21)

This year the VA team managed to put a lot of improvements, especially in code inspections and better performance for large projects.

See the recent news on their blog:

-   [Visual Studio 2022 Support!](https://blog.wholetomato.com/2021/11/23/visual-studio-2022-support/?utm_source=Bartek&utm_medium=Leads%20Acquisition&utm_content=Article-Dec21&utm_campaign=Article-Dec21)
-   [Visual Assist 2021.4 is released! (And notes on Visual Studio 2022)](https://blog.wholetomato.com/2021/11/02/visual-assist-2021-4-is-released-and-notes-on-visual-studio-2022/?utm_source=Bartek&utm_medium=Leads%20Acquisition&utm_content=Article-Dec21&utm_campaign=Article-Dec21)
-   [Unreal Engine ‘Quality Of Life’ in Visual Assist 2021.2](https://blog.wholetomato.com/2021/07/15/unreal-engine-quality-of-life-in-visual-assist-2021-2/?utm_source=Bartek&utm_medium=Leads%20Acquisition&utm_content=Article-Dec21&utm_campaign=Article-Dec21)

### ReSharper C++

[ReSharper C++](https://www.jetbrains.com/resharper-cpp/) is a Visual Studio productivity extension for C++ developers. It enhances the built-in features of Visual Studio, like refactoring, code analysis, navigation, and others.

[![](https://www.cppstories.com/2021/images/resharper.png)](https://www.jetbrains.com/resharper-cpp/)

In 2021, ReSharper C++ added support for the most recent C++20 language features and provided quick fixes to modernize the codebase automatically. The extension brought support for many rules from the C++ Core Guidelines and received extended capabilities for Unreal Engine game developers, like creating UE classes from templates without launching Unreal Editor.

A detailed summary of this year’s changes can be found here: [What’s New in ReSharper C++](https://jb.gg/6xi961).

### CLion

[CLion](https://www.jetbrains.com/clion/) is a cross-platform IDE for C and C++ by JetBrains. It works for projects in a wide range of fields, including trading and banking, embedded systems and AI, and many others.

![](https://www.cppstories.com/2021/images/clion.png)

In 2021, CLion extended the scope of its lifetime analysis to the translation unit and doubled the coverage of the MISRA C 2012 and MISRA C++ 2008 specifications. CMake presets and GNU Autotool projects are also now supported. The debugger received lots of enhancements and RTOS debugging was addressed, with dedicated tables and data now available in debug mode. CLion now features Code With Me, a new JetBrains service for collaborative development and pair programming, and it now supports the new [remote development workflow](https://jb.gg/ad6vt9). A detailed summary of this year’s changes can be found here: [What’s New in CLion](https://jb.gg/rtge2t).

#### Clang Power Tools

For Visual Studio, you can use [Clang Power Tools - @Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=vs-publisher-690586.ClangPowerTools). Developed by Victor Ciura ([@ciura_victor](https://twitter.com/ciura_victor)) and his Team.

Clang Power Tools is a free Visual Studio extension helping C++ developers modernize and transform their code to C++14/17/20 standards by using LLVM’s static analyzer and CppCoreGuidelines.

![](https://www.cppstories.com/2021/images/clangpowertools.png)

This year, in February, the team announced that the tool is now free for all users. See their blog post: [Next steps for Clang Power Tools](https://clangpowertools.com/blog/next-steps-for-clang-power-tools.html).

#### Clang Tools

Clang/LLVM powers many great utilities! For example:

-   [Clang-Tidy](https://clang.llvm.org/extra/clang-tidy/)
-   [Clang-Include-Fixer](https://clang.llvm.org/extra/clang-include-fixer.html)
-   [AddressSanitizer](https://clang.llvm.org/docs/AddressSanitizer.html)
-   [MemorySanitizer](https://clang.llvm.org/docs/MemorySanitizer.html)

#### Compiler Explorer

[**Compiler Explorer**](https://godbolt.org/), created by Matt Godbolt, is an interactive tool that lets you type code in one window and see the results of its compilation in another window.

Among many cool features, this year, Matt Godbolt’s team introduced a way to use CE with multiple files and manage them via CMake scripts! This is called “IDE mode”.

See this excellent tutorial: [Compiler Explorer with Cmake–Gajendra Gulgulia : Standard C++](https://isocpp.org/blog/2021/10/compiler-explorer-with-cmake-gajendra-gulgulia).

I’ve been using this tool (along with Wandbox) to experiment with various C++ features and even separate tools (like clang-tidy). It offers a way to check code against multiple compilers or libraries quickly.

#### Others:

**[Sourcetrail](https://www.sourcetrail.com/)**

It’s (or was…) a free and open-source, cross-platform source explorer. It was developed for several years, but unfortunately, the team decided to stop after releasing some final updates this year. See the blog post: [Discontinue Sourcetrail](https://www.sourcetrail.com/blog/discontinue_sourcetrail/)

#### Package Managers:

[**Conan**](https://www.conan.io/)

The open-source, decentralized and multi-platform package manager. Version 1.43 available this year. See their recent blog posts:

-   [Conan 1.43: Start preparing your recipes for Conan 2.0…](https://blog.conan.io/2021/12/21/New-conan-release-1-43.html)
-   [Conan 1.42 : New Conan XcodeDeps multi-config generator for Xcode…](https://blog.conan.io/2021/11/10/New-conan-release-1-42.html)
-   [Achievement Unlocked: Conan Center Hits 1,000 Recipes (and Counting)](https://blog.conan.io/2021/09/22/1000-recipes-call.html)

[**Microsoft/vcpkg: VC++ Packaging Tool**](https://github.com/Microsoft/vcpkg)

An open source C++ Library Manager for Windows, Linux, and MacOS. See the latest articles and releases:

-   [Bootstrap your dev environment with vcpkg artifacts - C++ Team Blog](https://devblogs.microsoft.com/cppblog/vcpkg-artifacts/)
-   [All vcpkg enterprise features now generally available: versioning, binary caching, manifests and registries - C++ Team Blog](https://devblogs.microsoft.com/cppblog/all-vcpkg-enterprise-features-now-generally-available-versioning-binary-caching-manifests-and-registries/)
-   [How to start using registries with vcpkg - C++ Team Blog](https://devblogs.microsoft.com/cppblog/how-to-start-using-registries-with-vcpkg/)

## Code Analyzers:

Various static code analyzers are available for C++. They range from simple checkers to super-advanced systems. The tools make it possible to detect problems early, improve code style, and add security bounds. While C++ is a complex language to parse, the analyzers heavily enhanced and are state-of-the-art tools in recent years.

### PVS-Studio

PVS-Studio is a static code analysis solution that detects errors in C++ programs on Windows, Linux, and macOS. Available with popular IDEs, including CLion. Run it locally or in the cloud.

![](https://www.cppstories.com/2021/images/pvs.png)

PVS-Studio’s developers implemented [intermodular analysis of C++ projects](https://pvs-studio.com/intermodular_analysis_cpp) and supported [security and safety](https://pvs-studio.com/sast_solution) standards, including Misra C.

In December 2021, PVS-Studio released version 7.16. To learn more, click here: [PVS-Studio 7.16, expanding the horizons: Misra C, Visual Studio 2022, .NET 6](https://pvs-studio.com/7.16).

Use the **cppstories2021** promo code and [get a 30-day PVS-Studio license](https://pvs-studio.com/download) for your project.

### SonarQube

[SonarQube](https://www.sonarqube.org/features/multi-languages/cpp/?utm_medium=paid&utm_source=cppstories&utm_campaign=cpp&utm_content=eoynewsletter) is an open-source platform developed by SonarSource for continuous inspection of Code Quality to perform automatic reviews with static analysis of code to detect bugs, code smells, and security vulnerabilities on 29 programming languages. SonarQube also supports the latest versions of C++!

[![](https://www.cppstories.com/2021/images/sonarqube.png)](https://www.sonarqube.org/features/multi-languages/cpp/?utm_medium=paid&utm_source=cppstories&utm_campaign=cpp&utm_content=eoynewsletter)

[In a recent blog article](https://blog.sonarsource.com/modernizing-your-code-with-cpp20?utm_medium=paid&utm_source=cppstories&utm_campaign=cpp&utm_content=eoynewsletter), the SonarSource team noted that they already have 28 C++20-specific rules in the latest releases of all of their products, including SonarQube, (with many more in development) aiming to make your coding easier and your code safer and more performant. Take a look and see what you can try today.

### SonarLint

[SonarLint](https://www.sonarlint.org/?utm_medium=paid&utm_source=cppstories&utm_campaign=cpp&utm_content=eoynewsletter) is a free IDE extension (for most IDEs out there) that highlights bugs, code smells and security vulnerabilities directly in the IDE as you write code, with clear remediation guidance.

[![](https://www.cppstories.com/2021/images/sonarlint.png)](https://www.sonarlint.org/?utm_medium=paid&utm_source=cppstories&utm_campaign=cpp&utm_content=eoynewsletter)

Its most recent release brings support for [‘Quick Fixes’](https://rules.sonarsource.com/cpp/quickfix/?utm_medium=paid&utm_source=cppstories&utm_campaign=cpp&utm_content=eoynewsletter) in CLion. For over 40 rules (unique and not available in the IDE or an improved version!) you can find and easily repair issues in your C and C++ code. It also includes additional C++ rules to help you avoid pitfalls when using new C++20 features.

You can visit the SonarLint [What’s New page](https://www.sonarlint.org/whats-new?utm_medium=paid&utm_source=cppstories&utm_campaign=cpp&utm_content=eoynewsletter) to see all the latest news about the free tool.

#### Others:

-   **CppCheck** - it’s a static analysis tool for C/C++ code, this year at version 2.6, see the [release notes](http://cppcheck.net/#news).
-   **CppDepend** - this year we have version CppDepend v2021.1 - [What’s new in CppDepend!](https://www.cppdepend.com/cppdependv2021)
-   **Deleaker** - it’s an extension for all major IDEs and a standalone application for memory leak detection - memory, GDI, and handles. Supports C++, C#, .NET and Delphi. See the latest [release notes](https://www.deleaker.com/changelog.html).

## Conferences

Fortunately, this year, some conferences tried to open their physical venues or go hybrid. This is a good opportunity to target larger audiences and offer a way to get most of the content on flexible terms.

Have a look at this link to ISO C++ page with all registered conferences around the world: [Conferences Worldwide, C++FAQ](https://isocpp.org/wiki/faq/conferences-worldwide/).

Some notable conferences in 2021:

#### CppCon 2021

October 25 till 29 (usually it was in late September), hybrid model.

You can watch keynotes, and other videos through this page: [https://pages.jetbrains.com/cppcon2021](https://pages.jetbrains.com/cppcon2021)

**Trip Reports:**

-   Inbal Levi [CppCon 2021 Trip Report](https://inballevi.medium.com/cppcon-2021-trip-report-22b056118ea9).
-   Javier Estrada [CppCon 2021 Virtual Trip Report](https://javierestrada.blog/2021/10/30/cppcon-2021-virtual-trip-report-a-user-story/).
-   Shafik Yaghmour [CppCon 2021 Trip Report](https://shafik.github.io/c++/learning/2021/10/31/cppcon2021_trip_report.html).
-   Jens Weller [Tripreport: virtual CppCon 2021 on Meeting C++](https://www.meetingcpp.com/blog/items/Tripreport--virtual-CppCon-2021.html).
-   Timur Doumler [CppCon 2021 trip report for JetBrains](https://blog.jetbrains.com/clion/2021/11/cppcon-2021-trip-report/).

#### Meeting C++ 2021

10 - 12th November 2021, fully online

[https://meetingcpp.com/2021/](https://meetingcpp.com/2021/)

#### C++ Russia

15 Nov - 18 Nov

It’s a conference with several tracks of in-depth technical talks devoted to C++. [https://2021.cppconf.ru/en/](https://2021.cppconf.ru/en/)

#### C++ Now

May 2–7

You can watch video recordings through the following pages:

-   [C++Now 2021 Videos | C++Now](https://cppnow.org/announcements/2021/05/2021-videos/)
-   [C++Now 2021 by Jetbrains](https://pages.jetbrains.com/cppnow2021)

#### ACCU 2021

[ACCU 2021](https://accu.org/conf-previous/accu2021/) - It Happened between March 9 to March 14; it was a virtual event.

See the recordings:

-   [ACCU 2021 Day 4 - playlist](https://www.youtube.com/watch?v=UsSmA62eQwY&list=PL9hrFapz4dsO5gFBxBliVZ-dgGCfQFQPu)
-   [ACCU 2021 Lightning Talks](https://www.youtube.com/watch?v=fZ_zPKscmEk&list=PL9hrFapz4dsMRhLdizfMea8OMmRj-mXHh)

## Community & User Groups

User groups are a chance for you to meet other C++ programmers, share your experience and learn new things. I highly recommend visiting such groups regularly… or at least once in a while.

If you don’t have a User Group close to your place (but please check [User Groups Worldwide](http://meetingcpp.com/usergroups/)), you can also participate in:

-   C++ Slack channel: [https://cpplang.now.sh/](https://cpplang.now.sh/)
-   [#include C++](https://www.includecpp.org/)

Additionally, Meeting C++ created Meeting C++ Online - a global monthly event where you can join and watch amazing C++ presentations. See it here: [Meeting C++ online](https://meetingcpp.com/mcpp/online/).

Jens Weller also organizes [Meeting C++ online - job fair](https://meetingcpp.com/mcpp/online/jobfair.php), and it’s an opportunity for you if you want to see for some new roles and get experience with new companies.

#### No Diagnostic Required show and C++ Annotated digest

For dynamic summaries of the latest developments from the C++ ecosystem, standardization news, and popular articles, take a look at the No Diagnostic Required YouTube show and podcast run by Anastasia Kazakova and Phil Nash. If you prefer to read your news, you can find written versions of our digests in the C++ Annotated emails and blog posts.

![](https://www.cppstories.com/2021/images/cppannotated.png)

-   [Podcast](https://nodiagnosticrequired.tv/),
-   [YouTube show](https://www.youtube.com/channel/UCJZdS1wIqASD1MVrJyX8M2Q),
-   [Digest](https://jb.gg/16p7dl).

## Books

A few selected books that arrived in 2021 (or late 2020):

_Disclaimer: Links in the table are affiliate links to Amazon._

| Name | Release Date |
| --- | --- |
| [Object Lifetime Puzzlers - Book 1](https://amzn.to/3Fow4WZ) by Jason Turner | December |
| [Beautiful C++: 30 Core Guidelines…](https://amzn.to/3yqv4ie) by J. Guy Davidson, Kate Gregory | December |
| [Discovering Modern C++ 2nd Edition](https://amzn.to/3yr1IjI) by Peter Gottschling | December |
| [Embracing Modern C++ Safely](https://amzn.to/3oUwpKX) by by J. Lakos, V. Romeo, R. Khlebnikov, A. Meredith | December |
| [The Art of Writing Efficient Programs](https://amzn.to/3pV2RMN) by Fedor G. Pikus | October |
| [Modern C++ for Absolute Beginners](https://amzn.to/3yu0B2T) by Slobodan Dmitrović | July |
| [C++20: Get the Details](https://amzn.to/3EZ0L4M) by Rainer Grimm | April |
| [Software Architecture with C++](https://amzn.to/3erCitN) by A. Ostrowski and P. Gaczkowski | April |
| [Professional C++ 5th Edition](https://amzn.to/3E15pOi) by Marc Gregoire | April |
| My [C++ Lambda Story](https://amzn.to/3H15dAL) in Print | February |
| [C++ Best Practices](https://amzn.to/3dUXUOd) by Jason Turner | January |
| [Performance Analysis and Tuning on Modern CPUs](https://amzn.to/3eyZPZr) by Denis Bakhvalov | November 2020 |
| [Beginning C++20 6th](https://amzn.to/3m8ZTD4), Ivor Horton and Peter Van Weert | October 2020 |

Plus, there is ongoing work for another C++20 Book by Nicolai M. Josuttis: [**“C++20 - The Complete Guide”**](https://leanpub.com/cpp20/c/5b1IaHdR1Xi2-10).

#### Promotions!

Exclusively for this article Rainer Grimm from [modernescpp.com](https://modernescpp.com/) offers **30% off** for his ebook on C++20! Grab it here:

-   [C++20: Get the Details by Rainer Grimm](https://leanpub.com/c20/c/Ri8fT8GdzLl1) @Leanpub **30% off** (valid till 7th January 2022)

Nicolai M. Josuttis offers the following coupon code:

-   [C++20 - The Complete Guide](https://leanpub.com/cpp20/c/5b1IaHdR1Xi2-10) @Leanpub - **only 16.9$** for his latest book (valid till 15th January 2022).

You can also grab my books:

-   [C++17 in Detail @Leanpub](https://leanpub.com/cpp17indetail/c/cpp2021) - **30% off**
-   [C++ Lambda Story @Leanpub](https://leanpub.com/cpplambda/c/cpp2021) - **22% off**

#### Notes and links:

-   [Software Architecture with C++, Book Review - C++ Stories](https://www.cppstories.com/2021/cpp-arch-book/)
-   [“Professional C++, 5th Edition” Released « Marc Gregoire’s Blog](http://www.nuonsoft.com/blog/2021/02/21/professional-c-5th-edition-released/)
-   [Book “Beginning C++20” « Marc Gregoire’s Blog](http://www.nuonsoft.com/blog/2020/12/26/book-beginning-c20/)

## Popularity

C++ seems to have stable growth in various programming languages' “popularity” charts this year.

Have a look:

![](https://www.cppstories.com/2021/images/cpp_popularity_2021.png)

The image is based on data from [Stack Overflow survey](https://insights.stackoverflow.com/survey/2021#technology) and [Tiobe Index](https://www.tiobe.com/tiobe-index/).

It looks like C++ got a bit more love than last year! :)

Additionally, according to Github, Octoverse C++ is in 7th position (last year it was also 7th place), see [here](https://octoverse.github.com/#top-languages-over-the-years).

## Your Input & Survey

On 20th December, I started my annual survey about the use of C++ in the last year. I got 782 votes, thank you!

Let’s make some summary and tables from your answers :)

#### C++ Standard Used

On a daily basis, which C++ Standard do you use?

| Answer | 2021 | 2020 | 2019 | 2018 |
| --- | --- | --- | --- | --- |
| Pre C++11 | 7.5% | 8.4% | 10.3% | 20% |
| C++11 | 25.6% | 25.5% | 30.3% | 41% |
| C++14 | 28% | 28.6% | 35% | 42% |
| C++17 | 66.1% | 64.4% | 62.4% | 44% |
| C++20 | 28.8% | 20.4% | 9.2% | n/a |

(The numbers for the above do not sum to 100%)

![C++ Use 2021 vs 2020](https://www.cppstories.com/2021/images/cpp21_use.png)

As we can see, fewer and fewer people use pre C++11. The same goes for C++11… Yet even in 2021, around 1/4 of C++ devs don’t have the luxury to work with the latest Standard.

C++17 dominates and rose from 44% in 2018 to more than 66% today. The trend for C++20 is on the way to taking over C++17 in two or more years.

#### Experience with C++17

What’s your experience with C++17?

| Answer | 2021 | 2020 | 2019 |
| --- | --- | --- | --- |
| experimenting with C++17 | 28.9% | 34.9% | 39.4% |
| only read basic information | 11.4% | 9.4% | 13.4% |
| already using in production | 56.6% | 52.2% | 41.6% |
| don’t know any of its feature | <1% | 1.6% | 2.6% |

C++17 becomes a production-ready standard, so fewer people experiment with it and move to the production code. GCC 11 also made C++17 a default dialect.

#### Experience with C++20

What’s your experience with C++20?

| Answer | 2021 | 2020 | 2019 |
| --- | --- | --- | --- |
| experimenting with C++20 | 35.7% | 35.6% | 29.3% |
| only read basic information | 44.1% | 50.8% | 59.8% |
| already using in production | 12.8% | 6.8% | n/a |
| don’t know any of its feature | 6% | 5.2% | 9.1% |

#### Compilers Used

What compiler do you use?

| Answer | 2021 | 2020 | 2019 |
| --- | --- | --- | --- |
| GCC | 76% | 70.3% | 75.6% |
| Clang | 51.8% | 49.6% | 58.7% |
| MSVC | 54.1% | 58.5% | 56.3% |
| Intel Compiler | 2.3% | 2.8% | 3.1% |
| C++ Builder | 2.2% | 3% | 1.2% |

(The numbers for the above do not sum to 100%)

#### What IDE do you use for C++ projects

New question for 2021!

| Answer | 2021 |
| --- | --- |
| Visual Studio | 48.8% |
| Visual Studio Code | 47.1% |
| CLion | 18.5% |
| C++ Builder IDE | 2% |
| Eclipse | 5.8% |
| Vim/Emacs | 26.9% |
| QT Creator | 15.7% |
| Notepad++ | 7.4% |
| XCode | 6.1% |

#### What additional tools do you use?

| Answer | 2021 | 2020 | 2019 |
| --- | --- | --- | --- |
| Debugger | 80.8% | 77% | 83.6% |
| Sanitizers | 38.9% | 31.9% | 40.4% |
| Static Code Analysis | 58.7% | 60.9% | 55.7% |
| Profilers | 49.1% | 53.4% | 56.8% |
| Clang Format | 49.4% | 43.3% | 49.3% |
| CMake | 67.3% | 62.3% | 66% |
| Package Managers | 26.2% | 23.2% | 21.4% |

(The numbers for the above do not sum to 100%)

#### Best thing that happened in 2020:

Answers from this open question, based on popularity (I tried to group similar things), no special order:

-   CppCon
-   C++20 standardization and Compiler support for C++20
-   Modules from C++20 have big impact on projects
-   Full Compiler support for C++17
-   Conferences: Meeting C++, Corecpp, CpponSea, C++ Russia, C++Now, and a lot of virtual C++ meetups
-   Progress on C++23
    -   std::expected,
    -   The deducing this paper made it into C++23,
    -   std::print,
    -   std::executors proposal
-   books like: “A Tour of C++"”, “Introduction to programming with C++ for engineers” by Boguslaw Cyganek, Wiley, “Clean C++20” by Stephan Roth, Professional CMake: A Practical Guide, Mastering the C++17 STD by Arthur O’Dwyer
-   C++20 books: C++17, and C++20 books from Rainer Grim, Andreas Fertig and Nicolai M. Josuttis
-   Release of Visual Studio 2022, improvement of lifetime profile in VS
-   Steady improvement of the language
-   Overwhelmed by the Standard or hard to follow
-   Better tools, 4, Unreal Engine 5, Godot Engine, docker, gcc 11, mold, Conan, clang-format, VCPKG, cmake-init, Package Managers got better, ASan support in MSVC, RAD Studio 11, Clion, VS Code
-   Better libs: Filesystem library for cross-platform Windows-Linux programming, IDK, QT 6.2, SYCL
-   Good resources: such as fluentcpp, cppcast, Jason Turner videos, Klaus Iglberger’s software design talks, Pluralsight courses, C++ Guides
-   Compiler Explorer (godbolt.org) just keeps getting better and better
-   Remote C++ Work and online talks available for a lot more people.
-   C++ renaissance in various ways, large scale applications with C++
-   In overall becomes more friendly

A good summary:

> C++20 is being used more and more, and C++ is still a top programming language. For me, first started programming in C++ circa 1992. To me C++ is the Best Programming Language Ever. And I appreciate all the work people like yourself contribute to C++. The best thing about C++ in 2021: we are still here programming in C++ with C++20 with no end in sight.

Additionally, it’s great to hear such news like

-   Completing a C++ course (or courses),
-   Role change, promotions
-   contribution to some open source project
-   Convinced leadership to bump up to cpp17

There were also many positive opinions about the blog and the newsletter! Thank you!

> “I read your newsletter, so it seems to be the best thing…”

> “Your website gave me very good info about c++.”

#### Other surveys:

My survey is not the most important :) Have a look at other larger surveys run by those companies:

-   [C++ Ecosystem in 2021: 1 in 5 C++ developers are using C++20 and a third of us are not writing any unit tests at all, and other facts | The CLion Blog](https://blog.jetbrains.com/clion/2021/07/cpp-ecosystem-in-2021/)
-   [Results summary: 2021 Annual C++ Developer Survey “Lite” : Standard C++](https://isocpp.org/blog/2021/04/results-summary-2021-annual-cpp-developer-survey-lite)
-   [Stack Overflow Developer Survey 2021](https://insights.stackoverflow.com/survey/2021)
-   [The Meeting C++ Community Survey results for 2020](https://meetingcpp.com/blog/items/The-Meeting-Cpp-Community-Survey-results-for-2020.html)

## What Expert says

As a bonus, here are a couple of opinions from C++ experts about the past year:

> “It’s exciting to see C++ ecosystem in 2021 moving towards having a standard toolset. CMake has grown from 34% in 2017 to 55% in 2021, becoming the absolute leader several years ago. Clang is adopted by many tool vendors and has evolved because of the community, with ClangFormat and Clang-Tidy tools seen as the de-facto Standard. meanwhile, language developers considers toolability aspect of the C++ features crucial for further adoption among everyday C++ developers.”
> 
> **Anastasia Kazakova**, [@anastasiak](https://twitter.com/anastasiak2512)

> “2021 continued to be challenging in terms of global pandemic. But the C++ community is very creative and continues to collaborate well. We have been fortunate to have great people that share their knowledge, publish books, write articles and run user groups. For me, the C++ twitter community is fun and very supportive. I enjoy running the San Diego C++ meetup and hoping to get back to in-person meeting very soon.”
> 
> **Yacob (Kobi) Cohen-Arazi**, [@kobi](https://twitter.com/kobi_ca)

> “For me, the biggest satisfaction in terms of C++ this year was finally full C++20 conformance in VisualStudio 2019 (latest versions) and the launch of VS 2022, my favorite C++ IDE and toolchain. This allowed my team to switch to C++20 in production and leverage the new language & library features for more succinct and robust code. After a disappointing 2020, C++ conferences in 2021 were back in full swing (no cancellations and lots of attendees), albeit in online format. CppCon was an interesting hybrid experience, but with limited onsite attendance.”
> 
> **Victor Ciura**, [@ciura_victor](https://twitter.com/ciura_victor)

> “My view of C++ in 2021 was strongly coloured by the future and the past. Helping write a book on the Core Guidelines reminded me of so many things we used to do and just don’t anymore because we have better ways.
> 
> Writing a course on what’s new in C++20 got me excited about all the things that will be so much easier in everyday code now. Time zones, composing range views, concept-powered error messages, spaceship operator - large and small these additions will keep making it easier to write fast and correct C++.”
> 
> **Kate Gregory**, [@gregcons](https://twitter.com/gregcons)

> “I am deeply worried about the path the C++ standard committee took in 2021. While not willing to fix a severe bug in the range-based for loop known for 10 years now, we prefer to release features that are not mature without allowing to fix them due to backward compatibility. Chaos and complexity grows significantly and it doesn’t look good for the future of C++.”
> 
> **Nicolai Josuttis**, [@NicoJosuttis](https://twitter.com/NicoJosuttis)

## Summary

Thanks for reading this long blog post!

So many things, events, tools, C++ features.

Are we in good shape in 2021?

It was a challenging year for many of us. We hoped that the pandemic would be over, but it’s not, and we need/had to adapt. The standardization process for C++23 was also hit, and it looks like it’s harder to process more extensive features. Yet the new Standard is in good condition, and in February, we should see its “feature freeze” state.

On the other hand, this year was very positive regarding the adoption of C++17 and C++20. C++17 is now a default dialect for GCC 11, and it’s now the “production-ready” Standard. As you can see in my survey reports, many developers use it daily. C++20 is now completed in almost all compilers, so it’s also an excellent time to introduce it into production.

The recent years are also filled with various improvements and new tools that improve our experience with the language. Better IDEs, smart suggestions core guideline checkers, linters, code analysers, clang format, sanitizers, package managers. While we could complain about the lack of tooling 10 years ago, this year, it’s not an option… and it’s even hard to keep up with all cool things that happen.

To summarize, my big things for 2021:

-   C++20 adoption
-   C++23 ongoing
-   Better tools

Additionally, as a side effect of current times, many companies opened for remote work, even after pandemic times. Such change gives us, C++ programmers, even more options for employment. Similarly, we can join many online meetings and take benefit of various meetups and conferences. While it’s probably not as good as physical events, it can reduce costs and open it for a larger audience.

Best wishes!

#### Your Turn

-   What do you think about C++ in 2021?
-   What was the most important event/news for you?
-   Did I miss something?

Join the discussion below the article and also in [this reddit/cpp thread](https://www.reddit.com/r/cpp/comments/rswgea/c_at_the_end_of_2021_a_detailed_overview/).