# Java memory
In memory the followings are stored
* instances,
* values,
* constants,
* field and method data,
* method codes,
* native methods,
* order of execution

and managed by the JVM.

Types of memories are
* class area,
* heap,
* stack,
* program counter register,
* native method stack memory.
## Stack memory
Used for executing methods.
Contains primitives and object references of methods.
Different stack block for every method - when the method is done the block gets removed.
## Heap memory
Hold all the objects that exists in the application.
Accessible from everywhere in the application using the address of the object (reference).
Objects on the heap contain privitive values are references to other objects <u>on the heap</u>.
# Pass-by-value
# Mutable & Immutable

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQyMTI4NTc4MV19
-->