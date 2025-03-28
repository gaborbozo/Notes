`FunctionalInterface` also known as Single Abstract Method (SAM), is an interface that **contains only one abstract method**. They are used to **represent functional expressions**, which are lambda expressions and method references.
> The compiler will enforce the single abstract method constraint, ensuring that the interface has only one abstract method.
# Closure
A closure in Java refers to a function or method that **"closes over"** variables from its surrounding lexical scope, meaning it captures and remembers the values of those variables. 
```java
final int a = 42;

// effectively final - not modified after initialization
int b = 42;

new Thread(() -> { System.out.println(a + b); }
```
This allows the function to access and use the captured variables even after the outer scope has finished executing.

Both **inner classes** and **lambda expressions** can close over variables.
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzI5Nzg3MDAxXX0=
-->