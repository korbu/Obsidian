### Named Return Value Optimization (NRVO)
A feature that allows us to optimize away the creation of a return value from a named object in a `return` statement. If we already have a local object that we return in a function by value, the compiler can use the object directly as a return value instead of copying or moving it.

Note that the *named return value optimization* differs from the [[#Return Value Optimization (RVO)]], which is the optimization for returning an object created on the fly in the `return` statement. The named return value optimization is optional in all versions of C++. If the compiler does not generate corresponding code, move semantics is used to create the return value.

### Return Value Optimization (RVO)
A feature that allows us to optimize away the creation of a return value from a temporary object that is created in the `return` statement. When we create the return value in the `return` statement on the fly and return it by value, the compiler can use the temporary object directly as a return value instead of copying or moving it.

Note that the *return value optimization* differs from the [[#Named Return Value Optimization (NRVO)]], which is the optimization for returning a named local object. The *return value optimization* was optional before C++17 but is mandatory since C++17 (*named return value optimization* is still optional).