# Default
# Public
# Protected
# Private
# Final
```java
// Immutable
final class A

// The reference to the object cannot be changed
// but it's internal state is changeable, assuming it's mutable.
final Object obj

// The method cannot be overridden.
final void do()

// The variable cannot be modified.
// A nested class can have a non-local variable
// It does not require synchronization to read
final int size
```
# Static
### Fields
They are created before the first reference and cease to exist after the last reference. They exist at the class level throughout the program's execution and can be referenced as `class.fieldName`.
### Methods
Similar to fields, they exist at the class level within an instance, and the reference is the same. Unlike "traditional" methods, they do not receive a `this` reference.
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzA3MjY4NTg2XX0=
-->