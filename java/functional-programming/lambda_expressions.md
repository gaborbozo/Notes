# Lambda expressions
`FunctionalInterface` enables the use of lambda expressions.
```java
public interface Printable(){
	void print();
}

// Basic lambda expression
// Inline definition
Printable lambdaPrintable = () -> {
		System.out.println("Hello World");
	};
lambdaPrintable.print();

// One single expression implementation
Printable lambdaPrintable = () -> System.out.println("Hello World"); 


public interface PrintableParameter(){
	void print(String string);
}

PrintableParameter lambdaPrintableParameter = (String s) -> System.out.println(s);
PrintableParameter lambdaPrintableParameter = (s) -> System.out.println(s);

// In case of having only one parameter brackets can be left
PrintableParameter lambdaPrintableParameter = s -> System.out.println(s);
```
```java
public interface PrintingParameter(){
	String print(String string);
}

PrintingParameter printingParameter = s -> {
	System.out.println(s);
	return s;
}

// In case if the method implementation is only one expression
// Java interprets that as a return value 
PrintingParameter printingParameter = s -> s;
```
In Java, some of the **built-in functional interfaces** include `Runnable`, `Supplier`,`Consumer`, `Callable`, `Function` and `Comparator`.
# Exceptions
In case of using lambda expression to implement an interface, the interface does not allow the declaration of exceptions in its methods, meaning we can not place `throws` clause in the lambda expression.

However `unchecked exceptions` can be thrown in lambda expressions without explicitly declaring `exception` handling.

Caught exceptions
```java
MyFunctionalInterface lambda = () -> {
    try {
        // Code that may throw an exception
    } catch (Exception e) {
        throw new MyException("An error occurred.", e);
    }
};
```
# Common `lambdas`
## Runnable(`run`) $\big(\emptyset\rarr\emptyset\big)$
`Runnable` is implemened by `Thread` class
This interface is designed to provide a common protocol for objects that wish to execute code while they are active.
The `Runnable` interface should be implemented by any class whose instances are intended to be executed by a thread.
```java
Runnable print = () -> System.out.println("Hello world");
print.run();
```
## Supplier(`get`) $\big(\emptyset\rarr T\big)$
Represents a function that takes no arguments but returns a value (`<T>`).
This function is used when we want to pass a function that generates a value to another function or method.
It is also used for lazy evaluation, where an expression is deferred until it's needed. 
```java
Supplier<T> rand = () -> new Random().nextInt();
rand.get();
```
## Consumer(`accept`) $\big(T\rarr\emptyset\big)$
Represent an operation that takes in a single argument and does not return any result.
Tipically used to pass a behaviour as an argument to methods that need to perform some operation on an object or a collection of objects.
```java
Consumer<String> printToConsole = s -> System.out.println(s);  
printToConsole.accept("Hello!");
```
## Callable(`call`) $\big(\emptyset\rarr T/\text{exception})$
Similar to `Runnable` but differs in that it can return a result and can throw checked exception.
Used in situations where a task needs to be executed asynchronously and retrieve the result of that task later on
```java
import java.util.concurrent.Callable;
import java.math.BigInteger;

public class FactorialCalculator implements Callable<BigInteger>
{ 
	private  int number;
	
	public FactorialCalculator(int number) { 
		this.number = number; 
	} 

	public BigInteger call() { 
		BigInteger  result  = BigInteger.valueOf(1); 
	
		for (int  i  =  1; i <= number; i++) { result = result.multiply(BigInteger.valueOf(i)); } 

		return result; 
	}
}

public class Main {  
	public static void main(String[] args) throws Exception {  
		FactorialCalculator factorialCalculator = new FactorialCalculator(5);  
  
		ExecutorService executor = Executors.newSingleThreadExecutor();  
		Future<BigInteger> future = executor.submit(factorialCalculator);  
		while (!future.isDone())
			System.out.println("waiting");    
		System.out.println(future.get());
	
	// Wrong it will calculate on current thread
	BigInteger currentThreadCalculated = factorialCalculator.get();
	}  
}
```
## Function(`apply`) $\big(T_1\rarr T_2\big)$
Represents a function that takes in one argument of type `T` and returns a result of type `R`.
Input and output types can be the same.
Usually used to transform data or process some input to produce an output. Can be used a wide variaty of operations such as mapping, filtering, converting etc.
```java
Function<String,Integer> strToInt = Integer::valueOf;
System.out.println(strToInt.apply("42"));
```
## Comperator(`compare`) $\big(T,T\rarr \text{integer})$
Represent a comperation between two `T` objects and returns an `Integer`.
Typically used in conjunction with sorting algorithms.
```java
Comparator<String> comparator = (s1,s2) -> {  
if (s1.equals(s2))
	return 1;  
return 0;  
};  
  
System.out.println(comparator.compare("A","Ab"));
```
## Predicate(`test`) $\big(T\rarr \text{boolean})$
Represents a function that takes one argument and returns a boolean value.
It is commonly used for filtering or testing objects based on some condition.
Predicates **can be composed using various default methods** provided by the interface, such as and(), or(), negate(), etc.
```java
List<String> words = Arrays.asList("apple", "banana", "cherry", "date");
Predicate<String> startsWithAPredicate = s -> s.startsWith("a");  
  
List<String> filteredWords = words.stream()  
.filter(startsWithAPredicate)  
.collect(Collectors.toList());  
  
System.out.println(filteredWords);


Predicate<Integer> greaterThanTen = x -> x > 10;  
Predicate<Integer> lessThanTwenty = x -> x < 20;  
Predicate<Integer> betweenTenAndTwenty = greaterThanTen.and(lessThanTwenty);

System.out.println(betweenTenAndTwenty.test(15));
```
## BiFunction(`apply`) $\big(T_1,T_2\rarr T_3)$
Represents a function that takes in two arguments of type `T`, `A` and returns a result of type `R`.
It is often used to implement functions that take two arguments and return a result based on those arguments.
```java
BiFunction<String,String,String> concat = (str1, str2) -> str1 + str2; 
System.out.println(concat.apply("Hello, ", "world!"));
```
It is also provides some default methods such as `andThen()`  which allow chainhg of functions.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzI1OTI1NDMxLC00OTU5MDUzMjhdfQ==
-->