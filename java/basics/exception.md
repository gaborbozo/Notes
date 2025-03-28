# Exceptions
An `exception` is an event that occurs during the execution of a program and disrupts the normal flow of instructions
# Try-catch
```java
try{
	// Code may cause exception
} catch(Exception e){
	// Handling exception
} finally{
	// Runs every time
	// Except
	// If the program is terminated abnormally, such as by calling `System.exit()`.
	// If the JVM crashes or if the host operating system crashes.
	// If the `finally` block contains an infinite loop or blocks indefinitely (e.g., by calling `Thread.sleep()`), in which case the program will hang.
}
```
## Multiple catching 
```java
} catch(NumberFormatException e) {
	// Handle
} catch(NullPointerException e) {
	// Handle
}

// Multi catch statement
} catch(NumberFormatException | NullPointerException e) {
	// Handle
}
```
# Hierarchy
A type of exception put into catch block will only catch exceptions of that type or any subclasses of the type

`Exception` will catch everything
`Object - Throwable - Exception - RuntimeException - IllegalArgumentException - NumberFormatException`
# Propagation
When an exception is thrown and not handled in a method it is called an unhandled exception, meaning that the exception is not caught by any try-catch block and it will propogate up the call stack until
* it is caught by a higher-level catch block
* it reaches the top level and terminates the program
# Checked and unchecked
In Java, there are two types of Throwables
1. Errors
`OutOfMemoryError,StackOverflowError` etc.
2. Exceptions
`RuntimeException` and all of the subclasses of it are `unchecked` exceptions.
Every others are `checked` exceptions. 

`Checked` exceptions are exceptions that must be handled or declared at compile time in Java.
```java
try {
	FileReader reader = new FileReader(fileName);
} catch(FileNotFoundException e) {}


public void readFile() throws FileNotFoundException {
	FileReader reader = new FileReader(fileName);
}
```
`Unchecked` exceptions(`runtime` exceptions) are exceptions that not required to be handled or declared in a method's throws clause at compile time.
```java
String string = null;
System.out.println(string.length());
```
# Debug
## Breakpoints
During a breakpoints, program execution is suspended, allowing to inspect the program's state
* It is not possible to enter the next method call in line, as we have interrupted the program's process
* Other thing can not be done is changing the content of a code when interrupting

- Although we can check the values of local variables, it is not recommended to modify them, as this may affect the program's execution
- It is also not advisable to exit from the active method call, as this may also disrupt the program's process
- Deleting local variables from the stack is also not recommended, as this can affect the program's execution as well
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTEwOTMzODgzXX0=
-->