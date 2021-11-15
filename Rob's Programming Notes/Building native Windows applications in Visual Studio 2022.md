# VS 2022 and C++
1. Presented by Sy Brand of the C++ team.
2. Manage open-source libraries: https://vcpkg.io.
3. Porting and Upgrade Guide: https://aka.ms/cpp/upgrade.
4. Hot Reload for C++: https://aka.ms/hotreloadcpp.
5. WSL2 Support: https://aka.ms/cpp-wsl2
6. Experimental libFuzzer Support: 
	1. Pass `/fsantize=fuzzer`.
	2. See https://aka.ms/cpp/libfuzzer.
7. STL
	1. See https://github.com/microsoft/STL.
	2. See https://microsoft.github.io/STL.
8. The four main features of C++20:
	1. Ranges,
		1. `#include <ranges>`.
		2. `| std::views::*` methods, e.g., `transform`, `take`.
			1. Note the pipe character (`|`).
	2. Modules,
		1. Modules use `import`.
	3. Coroutines,
		1.  Coroutines are a generalization of a subroutine or a regular function.  It can pause or suspend during execution and then be resumed later (like `yield` in C#).
		2.  You do this using `co_yield` instead of `return`. This will pause execution, send the value back to the caller, and can be resumed again later.
		3.  So, you may want to put the code in this method in an infinite loop.
		4.  You have to add coroutine traits for this to work, otherwise you will get errors.
		5.  There is no built-in mechanism for coroutine traits in C++20 (there should be in C++23), so you may want to use an open-source implementation like his `tl::generator`.
	4. Concepts.
		1. These underlie Ranges.
9. VS 2022 also uses manifest files.
	1. Similar to npm for JavaScript.
	2. Declaratively describe our package.
	3. You can list dependencies in this file, including their versions.
	4. Name it vcpkg.json in the root of your project.
	5. In project settings, change "Use VcPkg Manifest" to "Yes".
10. The tl package uses the `.hpp` file extension instead of `.h`
	1. I should ==use `.hpp`==, too.

## To-Do
1. ==Work through Sy's example== C++20 code to get the hang of it.
2. ==Write up notes== about how C++20 modules work, including the placement of `#includes` above the `export` statement and adding `module;` at the top of the file.
3. Determine how to ==install VcPkg== for VS 2022.