# Locks in C++

**Created**: Friday, January 22, 2021 04:25:49 PM -05:00
**Modified**: Friday, January 22, 2021 04:59:30 PM -05:00


| <br /> | **Lock Type** | **Description** | **Counted?** | **Have Clear**<br /><br />**Thread Ownership** |
| --- | --- | --- | --- | --- |
| 1 | Spin locks | Spin locks are uncounted locks that have clear thread ownership. | No | Yes |
| 2 | Mutexes | Mutexes are counted locks that have clear thread ownership. | Yes | Yes |
| 3 | Critical Sections | Critical Sections are counted locks that have clear thread ownership. | Yes | Yes |
| 4 | Semaphores | Semaphores are counted locks that do not have clear thread ownership. | Yes | No |
| 5 | Events | Events are counted locks that do not have clear thread ownership. | Yes | No |

# SAL Annotations

https://docs.microsoft.com/en-us/cpp/code-quality/annotating-locking-behavior?view=msvc-160

## Locking Annotations

The following table lists the locking annotations.

| **Annotation** | **Description** |
| --- | --- |
| \_Acquires\_exclusive\_lock\_(expr) | Annotates a function and indicates that in post state the function increments by one the exclusive lock count of the lock object that's named by expr. |
| \_Acquires\_lock\_(expr) | Annotates a function and indicates that in post state the function increments by one the lock count of the lock object that's named by expr. |
| \_Acquires\_nonreentrant\_lock\_(expr) | The lock that's named by expr is acquired. An error is reported if the lock is already held. |
| \_Acquires\_shared\_lock\_(expr) | Annotates a function and indicates that in post state the function increments by one the shared lock count of the lock object that's named by expr. |
| \_Create\_lock\_level\_(name) | A statement that declares the symbol name to be a lock level so that it may be used in the annotations \_Has\_Lock\_level\_ and \_Lock\_level\_order\_. |
| \_Has\_lock\_kind\_(kind) | Annotates any object to refine the type information of a resource object. Sometimes a common type is used for different kinds of resources and the overloaded type is not sufficient to distinguish the semantic requirements among various resources. Here's a list of pre-defined kind parameters:<br /><br /><br />\_Lock\_kind\_mutex\_<br />Lock kind ID for mutexes.<br /><br /><br />\_Lock\_kind\_event\_<br />Lock kind ID for events.<br /><br /><br />\_Lock\_kind\_semaphore\_<br />Lock kind ID for semaphores.<br /><br /><br />\_Lock\_kind\_spin\_lock\_<br />Lock kind ID for spin locks.<br /><br /><br />\_Lock\_kind\_critical\_section\_<br />Lock kind ID for critical sections. |
| \_Has\_lock\_level\_(name) | Annotates a lock object and gives it the lock level of name. |
| \_Lock\_level\_order\_(name1, name2) | A statement that gives the lock ordering between name1 and name2. Locks that have level name1 must be acquired before locks that have level name2. |
| \_Post\_same\_lock\_(expr1, expr2) | Annotates a function and indicates that in post state the two locks, expr1 and expr2, are treated as if they are the same lock object. |
| \_Releases\_exclusive\_lock\_(expr) | Annotates a function and indicates that in post state the function decrements by one the exclusive lock count of the lock object that's named by expr. |
| \_Releases\_lock\_(expr) | Annotates a function and indicates that in post state the function decrements by one the lock count of the lock object that's named by expr. |
| \_Releases\_nonreentrant\_lock\_(expr) | The lock that's named by expr is released. An error is reported if the lock is not currently held. |
| \_Releases\_shared\_lock\_(expr) | Annotates a function and indicates that in post state the function decrements by one the shared lock count of the lock object that's named by expr. |
| \_Requires\_lock\_held\_(expr) | Annotates a function and indicates that in pre state the lock count of the object that's named by expr is at least one. |
| \_Requires\_lock\_not\_held\_(expr) | Annotates a function and indicates that in pre state the lock count of the object that's named by expr is zero. |
| \_Requires\_no\_locks\_held\_ | Annotates a function and indicates that the lock counts of all locks that are known to the checker are zero. |
| \_Requires\_shared\_lock\_held\_(expr) | Annotates a function and indicates that in pre state the shared lock count of the object that's named by expr is at least one. |
| \_Requires\_exclusive\_lock\_held\_(expr) | Annotates a function and indicates that in pre state the exclusive lock count of the object that's named by expr is at least one. |

## SAL Intrinsics For Unexposed Locking Objects

Certain lock objects are not exposed by the implementation of the associated locking functions. The following table lists SAL intrinsic variables that enable annotations on functions that operate on those unexposed lock objects.

| **Annotation** | **Description** |
| --- | --- |
| \_Global\_cancel\_spin\_lock\_ | Describes the cancel spin lock. |
| \_Global\_critical\_region\_ | Describes the critical region. |
| \_Global\_interlock\_ | Describes interlocked operations. |
| \_Global\_priority\_region\_ | Describes the priority region. |

## Shared Data Access Annotations

The following table lists the annotations for shared data access.

| **Annotation** | **Description** |
| --- | --- |
| \_Guarded\_by\_(expr) | Annotates a variable and indicates that whenever the variable is accessed, the lock count of the lock object that's named by expr is at least one. |
| \_Interlocked\_ | Annotates a variable and is equivalent to \_Guarded\_by\_(\_Global\_interlock\_). |
| \_Interlocked\_operand\_ | The annotated function parameter is the target operand of one of the various Interlocked functions. Those operands must have specific additional properties. |
| \_Write\_guarded\_by\_(expr) | Annotates a variable and indicates that whenever the variable is modified, the lock count of the lock object that's named by expr is at least one. |

## Smart Lock and RAII Annotations

Smart locks typically wrap native locks and manage their lifetime. The following table lists annotations that can be used with smart locks and RAII coding patterns with support for move semantics.

| **Annotation** | **Description** |
| --- | --- |
| \_Analysis\_assume\_smart\_lock\_acquired\_ | Tells the analyzer to assume that a smart lock has been acquired. This annotation expects a reference lock type as its parameter. |
| \_Analysis\_assume\_smart\_lock\_released\_ | Tells the analyzer to assume that a smart lock has been released. This annotation expects a reference lock type as its parameter. |
| \_Moves\_lock\_(target, source) | Describes move constructor operation which transfers lock state from the source object to the target. The target is considered a newly constructed object, so any state it had before is lost and replaced by the source state. The source is also reset to a clean state with no lock counts or aliasing target, but aliases pointing to it remain unchanged. |
| \_Replaces\_lock\_(target, source) | Describes move assignment operator semantics where the target lock is released before transferring the state from the source. This can be regarded as a combination of \_Moves\_lock\_(target, source) preceded by a \_Releases\_lock\_(target). |
| \_Swaps\_locks\_(left, right) | Describes the standard swap behavior which assumes that objects left and right exchange their state. The state exchanged includes lock count and aliasing target, if present. Aliases that point to the left and right objects remain unchanged. |
| \_Detaches\_lock\_(detached, lock) | Describes a scenario in which a lock wrapper type allows dissociation with its contained resource. This is similar to how std::unique\_ptr works with its internal pointer: it allows programmers to extract the pointer and leave its smart pointer container in a clean state. Similar logic is supported by std::unique\_lock and can be implemented in custom lock wrappers. The detached lock retains its state (lock count and aliasing target, if any), while the wrapper is reset to contain zero lock count and no aliasing target, while retaining its own aliases. There's no operation on lock counts (releasing and acquiring). This annotation behaves exactly as \_Moves\_lock\_ except that the detached argument should be return rather than this. |

# See also

- [Using SAL Annotations to Reduce C/C++ Code Defects](https://docs.microsoft.com/en-us/cpp/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects?view=msvc-160)
- [Understanding SAL](https://docs.microsoft.com/en-us/cpp/code-quality/understanding-sal?view=msvc-160)
- [Annotating Function Parameters and Return Values](https://docs.microsoft.com/en-us/cpp/code-quality/annotating-function-parameters-and-return-values?view=msvc-160)
- [Annotating Function Behavior](https://docs.microsoft.com/en-us/cpp/code-quality/annotating-function-behavior?view=msvc-160)
- [Annotating Structs and Classes](https://docs.microsoft.com/en-us/cpp/code-quality/annotating-structs-and-classes?view=msvc-160)
- [Specifying When and Where an Annotation Applies](https://docs.microsoft.com/en-us/cpp/code-quality/specifying-when-and-where-an-annotation-applies?view=msvc-160)
- [Intrinsic Functions](https://docs.microsoft.com/en-us/cpp/code-quality/intrinsic-functions?view=msvc-160)
- [Best Practices and Examples](https://docs.microsoft.com/en-us/cpp/code-quality/best-practices-and-examples-sal?view=msvc-160)