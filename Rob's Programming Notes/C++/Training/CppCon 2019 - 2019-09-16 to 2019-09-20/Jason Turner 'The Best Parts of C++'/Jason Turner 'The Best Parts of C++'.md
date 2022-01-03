# Jason Turner "The Best Parts of C++"

**Created**: Monday, November 04, 2019 10:05:19 AM -05:00
**Modified**: Wednesday, December 29, 2021 03:51:14 PM -05:00


1. Day One - 09/16/2019
2. https://emptycrate.com/idocpp
3. Feature # 1: The C++ Standard
    1. First was C++98.
4. Feature # 2: `const`
5. Feature # 3: Deterministic Object Lifetime and Destruction (RAII)
    1. <mark style="background: #BBFABBA6;">If you're going to allocate memory, make your own class with a destructor.</mark>
6. Feature # 4: Templates
    1. <mark style="background: #FFF3A3A6;">What is Type Erasure?</mark>
    2. He mentions this at on Slide # 5.2.
    3. <mark style="background: #FFF3A3A6;">What does it mean that templates are Turing complete?</mark>
        1. Same slide as above.
        2. <mark style="background: #FFF3A3A6;">Why is this not good?</mark>
    4. <mark style="background: #FFF3A3A6;">What is copy elision?</mark>
        1. Slides # 5.4/5.5.
        2. <mark style="background: #BBFABBA6;">Use `vector` (or other containers?) instead of your own data types where possible.</mark>
        3. See Feature # 22 for more about copy elision!!!
7. <mark style="background: #BBFABBA6;">Feature # 5: Use `accumulate` (or other algorithms) where possible.</mark>
    1. Slides # 5.6 to 6.2.
    2. Everyone knows for\_each and accumulate.
    3. <mark style="background: #BBFABBA6;">set\<\></mark>
    4. <mark style="background: #BBFABBA6;">vector\<\></mark>
    5. <mark style="background: #BBFABBA6;">for_each</mark>
    6. <mark style="background: #BBFABBA6;">any_of</mark>
8. <mark style="background: #BBFABBA6;">Feature # 6: Use `std::array` when you know the size of your data structure at compile time.</mark>
    1. Slides # 6.4 to 7.2 (from Lenny Maiorani's negative cost abstraction).
9. Feature # 7: List Initialization
    1. Create a version of your templated function that takes 1, 2, 3 parameters, etc.
    2. <mark style="background: #BBFABBA6;">Use an initializer list to initialize all of your values.</mark>
    3. <mark style="background: #BBFABBA6;">You can even just return an initializer list!!!</mark>
    4. <mark style="background: #FFF3A3A6;">He did an entire 1 1/2 hour talk on "Initializer Lists Are Broken".</mark>
        1. [C++Now 2018: Jason Turner “Initializer Lists Are Broken, Let's Fix Them” - YouTube](https://www.youtube.com/watch?v=sSlmmZMFsXQ)
10. Feature # 8: Variadic Templates
    1. How do we avoid copy/pasting the 1, 2, 3, 4, 5 ,6 parameter versions?
    2. ![](/Attachments/1-48f0c8615f9846feb2740a924ce8fcd8.png)
    3. Absolutely critical for maintainable implementations of things like `std::function.`
        1. <mark style="background: #FFF3A3A6;">Why?</mark>
        2. Before C++11, you had to use boost::bp (vp? pp? you're asking the preprocessor to generate the code for you) or unroll the code by hand.
11. <mark style="background: #BBFABBA6;">Feature # 9: constexpr</mark>
    1. <mark style="background: #BBFABBA6;">Compile-time generation of code and data.</mark>
    2. <mark style="background: #BBFABBA6;">Use compile-time constants wherever possible, e.g. pi.</mark>
    3. You can even use a constexpr function to calculate pi.
12. <mark style="background: #BBFABBA6;">Feature # 10: auto</mark>
    1. What should the type of pi be?
        1. float?
        2. double?
        3. long double?
        4. I don't care.
        5. It depends.
        6. Jason falls into one of the last two categories.
    2. Automatic deduction of value types.
13. Feature # 11: Return type deduction for normal functions
    1. <mark style="background: #BBFABBA6;">Return an auto.</mark>
    2. Allows for the creation of powerful higher-order function constructs.
    3. He just did a C++ Weekly episode on this the week before this talk.
14. Feature # 12: Lambdas
    1. He has a std::map with a set of key/value pairs that he'd like to print.
    2. <mark style="background: #BBFABBA6;">Best practices (and Sean Parent) tell us "no raw loops".</mark>
    3. So, let's use an algorithm.
    4. C++03: for\_each
    5. We also need a function object, i.e. something that is callable.
        1. Callable(operator())
        2. Let's not talk about functors.
            1. <mark style="background: #FFF3A3A6;">Why not?</mark>
    6. If only there was some handy way of creating a callable thing for use with an algorithm.
    7. Lambdas!
    8. ![](/Attachments/1-60d50d684b7b4f5ba9a039569b813903.png)
    9. Lambdas allow us to create unnamed function objects which may or may not have captures.  We are not allowed to know the name of the type of a lambda.
    10. ![](/Attachments/1-bff84b696aa0410a99b646ff1b1f94ef.png)
15. Feature # 13: Generic and Variadic Lambdas
    1. If only there was some way to automatically deduce the types of lambda parameters…
        1. <mark style="background: #FFF3A3A6;">auto!</mark>
    2. ![](/Attachments/1-5ff2507e59d74cb2a45bfa6e5152cae0.png)
    3. ![](/Attachments/1-b18eada4c63e48e0a28ee4302f4b29c8.png)
16. <mark style="background: #BBFABBA6;">Feature # 14: Range-based for loops</mark>
    1. If only there was some simple way to iterate over all the values in a container…
    2. Range-based for loops
    3. ![](/Attachments/1-d42c8e25d2e7484aa300ee01d68820ee.png)
    4. Iterates over all elements in a container.
        1. <mark style="background: #BBFABBA6;">Works with anything that has begin() and end() members/functions, C-style arrays, and initializer lists.</mark>
17. <mark style="background: #BBFABBA6;">Feature # 15: Structured Bindings</mark>
    1. If only there was some way to make this data.first, data.second nonsense more readable.
    2. ![](/Attachments/1-665241eb2cd0433abdcf9ec1f5af2202.png)
    3. <mark style="background: #BBFABBA6;">These are parameters to a lambda. (Rob's comment)</mark>
    4. <mark style="background: #BBFABBA6;">Used to decompose a structure or array into a set of identifiers.  You *must* use auto and the number of elements must match.  There's no way to skip an element (as of C++17).</mark>
18. Feature # 16: Concepts
    1. The whole template syntax is a bit bulky.  Is there any way to simplify that?
    2. <mark style="background: #FFF3A3A6;">Who loves SFINAE?  Who knows what SFINAE is?</mark>
    3. ![](/Attachments/1-416e01c67d5f4347888aa9150675fe16.png)
    4. ![](/Attachments/1-bce9493bc48244ce946cd23e1eef9991.png)
    5. <mark style="background: #BBFABBA6;">Concepts are in C++20.</mark>
    6. concept is a new keyword, new syntax to get used to.
    7. <mark style="background: #BBFABBA6;">Concepts allow us to specify the requirements for a type, implicitly creating a template that constrains how a function can be used.</mark>
    8. <mark style="background: #FFF3A3A6;">The original idea for concepts comes from Alexander Stepanov.</mark>
19. Feature # 17: `std::string_view`
    1. ![](/Attachments/1-b0e31008a20240c492478344ec7696cd.png)
    2. ![](/Attachments/1-f41a8b70b56c455eb2bf0aa80f0fe308.png)
    3. <mark style="background: #BBFABBA6;">string_views are passed by value on purpose.</mark>
        1. <mark style="background: #BBFABBA6;">They are cheap to copy.</mark>
        2. He could have passed them by `const` value.
    4. ![](/Attachments/1-290f7bd28fe94719af6132383b9847fd.png)
    5. This code no longer creates a string at all if it's not necessary.
20. Feature # 18: Text Formatting
    1. `std::cout` is quite verbose, relatively slow, and difficult to reason about.  If only there was some easier way to format our output.
    2. In C++20, `std::format` has no way to print.
    3. But, it is generating a null-terminated string.
    4. However, `std::puts` is an extremely efficient way of writing out a null-terminated string with an implicit carriage return at the end of it.
    5. ![](/Attachments/1-532dd188c22e47f88715066c9559571e.png)
    6. ![](/Attachments/1-b003c222adc14e0cbfbea98d86e9965c.png)
21. Feature # 19: Ranges
    1. If only there was some way to not have to do this begin(map) and end(map) stuff when using algorithms…
    2. <mark style="background: #BBFABBA6;">Ranges!</mark>
    3. ![](/Attachments/1-a70337fece1b40d3b1133fad3c42f164.png)
    4. ![](/Attachments/1-164739ae3e724c8fa45463abbeef6239.png)
    5. <mark style="background: #FFF3A3A6;">I really need to try this out because I do NOT understand how this works!</mark>
    6. Note that you might use `std::format `instead of `std::cout` here, but he's not sure.
22. <mark style="background: #FFF3A3A6;">Feature # 20: Class Template Argument Deduction (review this entire topic!)</mark>
    1. <mark style="background: #BBFABBA6;">Prior to C++17, it used to just be function templates (not class templates).</mark>
    2. ![](/Attachments/1-35b8e83e067b473fa3ba3355598e6742.png)
    3. ![](/Attachments/1-f5d3a1edb7e14181a092d33efae32fca.png)
    4. We're just moving the return type into the return statement.
    5. If only there was a way to automatically deduce the type of the array being returned.
    6. ![](/Attachments/1-115ff03767844d0a85600b150da6143a.png)
    7. ![](/Attachments/1-4edf01c72da449e4add554e7356b27d9.png)
    8. For types like vector, it's only interesting.
    9. ![](/Attachments/1-e604641f599e446eb7a0956c37d7cc71.png)
    10. ![](/Attachments/1-56d57426e7cf4c3dab38a42e262aef22.png)
23. <mark style="background: #FFF3A3A6;">Feature # 21: rvalue References (review this entire topic!)</mark>
    1. ![](/Attachments/1-906ffbb185e34f98a2b85a8e3de6c1fe.png)
    2. ![](/Attachments/1-2d88bf1d58844755ab27cd7e07804d43.png)
24. Feature # 22: Guaranteed Copy Elision
    1. ![](/Attachments/1-212fd840b6fb431f9ad7e93a6889d63a.png)
    2. We have deleted the move constructor on line 3.
    3. And we have deleted the copy constructor on line 4.
    4. <mark style="background: #BBFABBA6;">This object should not be copyable or moveable.</mark>
    5. And yet he is returning it from a function on line 8.
    6. This code is required to compile in C++17.
    7. <mark style="background: #BBFABBA6;">This is neither a copy nor a move.</mark>
    8. He loves this!
    9. <mark style="background: #BBFABBA6;">It is two different ways of referring to the SAME object.</mark>
    10. <mark style="background: #FFF3A3A6;">(His slides are editable in Compiler Explorer!  How did he do that?)</mark>
    11. He goes into more detail about how this works in one of his talks later this week.
25. <mark style="background: #FFF3A3A6;">Feature # 23: Defaulted and Deleted Functions (review this entire topic!)</mark>
    1. ![](/Attachments/1-ea11dd2506844d7d806ec95008321911.png)
    2. This relies on copy elision.
    3. In C++98 it's a copy.
    4. In C++11 it's a move.
    5. <mark style="background: #BBFABBA6;">Potential double delete!</mark>
    6. ![](/Attachments/1-2b499e706efe4c51b8ef3bdcc4ec6e18.png)
    7. There are two different copies of the same pointer theoretically.
    8. <mark style="background: #BBFABBA6;">Hypothetically two different destructors that are going to be called.</mark>
        1. <mark style="background: #BBFABBA6;">Although it never actually happened that way in code this simple.</mark>
    9. ![](/Attachments/1-cf70c10b194044ec8a731a4c68710bb3.png)
    10. In C++11 it's now a move.
    11. A built-in move of a scalar type, a pointer, is implicitly a copy, so C++11 doesn't change anything.
    12. <mark style="background: #BBFABBA6;">We still get the double-free.</mark>
    13. ![](/Attachments/1-55a5e50dd04d4c889751fb5fceb0473e.png)
    14. This works in C++17.
    15. ![](/Attachments/1-d8f5db02cd41440198a4a1ae74ed2238.png)
    16. <mark style="background: #BBFABBA6;">You can delete ANY function!</mark>
26. Feature # 24: `std::unique_ptr` and `std::make_unique`
    1. ![](/Attachments/1-ac608123eb3b4f708350509422174233.png)
    2. <mark style="background: #BBFABBA6;">std::make_unique is just doing a heap allocation for you behind the scenes. (Rob's comment).</mark>
    3. ![](/Attachments/1-f3e821bebb614ea9abd0c0aa3a7a92d3.png)
    4. We didn't get `std::make_unique` until C++14.
        1. We got `std::make_shared` in C++11; leaving out `std::make_unique` was an oversight.
27. <mark style="background: #FFF3A3A6;">Feature # 25: Fold Expressions (review this entire topic!)</mark>
    1. ![](/Attachments/1-c052de21d1974307a95aa1936a9f637f.png)
    2. We need a way to sum this when we have **<span style="">variadic templates</span>**.
    3. ![](/Attachments/1-a5105e544f154053b779cd080264db90.png)
    4. ![](/Attachments/1-5f461ead00dd4dc9938121a5d0f16cb2.png)
    5. <mark style="background: #FFF3A3A6;">I don't understand this very well.</mark>
    6. He's abusing the initializer list here.
    7. Sean Parent and Eric Niebler first published this as a Twitter thread.
        1. <mark style="background: #FFF3A3A6;">Go find it.</mark>
        2. <mark style="background: #FFF3A3A6;">Is Eric's last name spelled right?</mark>
        3. <mark style="background: #FFF3A3A6;">Do I follow him on Twitter?</mark>
        4. <mark style="background: #FFF3A3A6;">What about Sean Parent?</mark>
    8. This is CONSIDERABLY faster to compile.
    9. He wouldn't say it's readable.
    10. The comma operator returns the right side (last most element), which in this case is the value 0.
        1. <mark style="background: #FFF3A3A6;">Read up on the comma operator!</mark>
    11. So 0 initializes the initializer list.
    12. He casts the initializer list to void to avoid an unused variable error (or something like that).
    13. ![](/Attachments/1-45fe4636e5b24c36a64b3bdfb6586857.png)
    14. Here he has expanded the type of result from auto to its full definition.
        1. <mark style="background: #FFF3A3A6;">Is using auto an error?</mark>
        2. <mark style="background: #FFF3A3A6;">I have no idea why he calls this "corrected".</mark>
    15. ![](/Attachments/1-6cd5fcb8181a40ecaff1a823ef5ba963.png)
    16. He thinks this is pretty neat.
    17. ![](/Attachments/1-182e6e6c26454fbd9ca91a26a93eedc4.png)
    18. He emphasized that this works with ANY common operator.
        1. &quot;It's weird the stuff you can do with fold expressions.&quot;
28. ![](/Attachments/1-44db533fde9e4272b91cebe418736349.png)

29. ![](/Attachments/1-b5d40954f0c24761a379dba36caefbdb.png)

30. ![](/Attachments/1-3425b4f91f054b4692d78b847b95c02f.png)

31. ![](/Attachments/1-d19361ee6f2a4b3fb7e9f3b987dc8f22.png)

32. ![](/Attachments/1-2e4f63078a2c41babd18dd4df995e01f.png)

33. ![](/Attachments/1-7122b93d84dc4bfb817d2990bf27fa80.png)
    1. <mark style="background: #FFF3A3A6;">Run clang modernize on your code!</mark>
34. ![](/Attachments/1-938bea88420148fcacccfc549d2a38d3.png)
    1. <mark style="background: #BBFABBA6;">Note that contracts were cut from C++20.</mark>
35. ![](/Attachments/1-6fa23f6578214d6996eec815ff9ad995.png)

    Jason Turner 
     • Co-host of CppCast https://cppcast.com 
     • Host of C++ Weekly https://www.youtube.com/c/JasonTurner-lefticus 
     • Projects 
     • https://chaiscript.com 
     • https://cppbestpractices.com 
     • https://github.com/lefticus/cpp_box 
     • https://coloradoplusplus.info 
     • Microsoft MVP for C++ 2015-present

36. ![](/Attachments/1-f6b2568038fe4cacb82934bb18ad1d74.png)

    Independent and available for training or contracting 
     -https://articles.emptycrate.com/idocpp

Watched on the plane flight to Seattle on 11/04/2019.