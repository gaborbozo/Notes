`FunctionalInterface` also known as Single Abstract Method (SAM), is an interface that contains only one abstract method. They are used to represent functional expressions, known as **lambda expressions** and method references.
> The compiler will enforce the single abstract method constraint, ensuring that the interface has only one abstract method.
# Closure
A closure in Java refers to a function or method that **"closes over"** variables from its surrounding lexical scope, meaning it captures and remembers the values of those variables. 
```java
final int a = 42;

// effectively final - not modified after initialization
int b = 42;

new Thread(() -> { System.out.println(a + b); }
```
**This is because lambda expressions may outlive the method in which they are defined**. Java wants to avoid unexpected behavior caused by changing variables in closures. **This restriction ensures thread safety and consistency**.
Both **inner classes** and **lambda expressions** can close over variables.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUwNTkyODUxMCwtMTc1NzQ1NTU1MCwxNT
Y4MjIyNzMxLDcyOTc4NzAwMV19
-->