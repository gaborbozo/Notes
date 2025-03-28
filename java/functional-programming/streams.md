# Streams
`Collections` are a group of related classes and interfaces that represent data structures such as lists, sets, and maps.
`Streams` allows us to process collections of elements in a **functional** and **declarative** way

`Stream` is an abstraction which focuses on the all insted of the parts
```java
// Imperative approach
List<Employee> employees = getEmployees();
double totalSalary = 0;
for (Employee employee : employees)
	if (employee.getDepartment().equals("IT"))
		totalSalary += employee.getSalary();


// Stream API approach
List<Employee> employees = getEmployees();
double totalSalary = employees.stream()
	.filter(employee -> employee.getDepartment().equals("IT")) 
	.mapToDouble(Employee::getSalary).sum();
```
# How they work
## Preparation - start with a collection.
* `Array` (`Stream.of`, `Arrays.stream`),`Set`,`List` (`myList.stream()`),`Map` etc.
* `iterate`, `intStream.range`

**Unlike data structures streams can be used only once**
> If the order of the data does not matter, the elements of the stream can be processed in parallel using `parallel()`.
Streams are one-time use, unlike data structures.
## Transformation - **intermediate** operations
At this point we can have as many streams as we want.
Instead of controlling every single aspect of the original `Collection` every abstraction represents a correspondation.
When invoking `.stream()` we can use the so called intermediate operations such as `filter`,`map`,`reduce`, `limit`, etc.
> Intermediate operations transform a stream into another and they are **lazily evaluated** (not executed until a terminal operation is called on the stream).
## Utilization - back to concrete  - **terminal** operations
* Using `forEach`, element by element 
* Transformed into a data structure `to...` an `array`, `list`, `map`
* Converted to a value:
  * For a single element of the stream
  * `Concatenated` as a `string`
  * `joining` Converted to a `number`
  * `count` Logical operations: `anyMatch`, `allMatch`, `noneMatch`
* Grouped into a Map: `...By`
* In general: `reduce`, `collect`
# Common preparation methods


# Common intermediate operations
### `filter`
Returns a stream consisting of the elements of this stream that match the given predicate.
```java
// [0, 2, 4, 6, 8]
IntStream.range(0,10).filter(x -> x % 2 == 0);
```
### `map`
Returns a stream consisting of the results of applying the given function to the elements of this stream.
```java
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
IntStream.range(0,10).map(x -> x + 1);
```
### `flatMap`
Returns a stream consisting of the results of replacing each element of this stream with the contents of a mapped stream produced by applying the provided mapping function to each element.
```java
Integer[][] matrix = {{3,2},{4},{1,5,6}};  

// [3, 2, 4, 1 , 5, 6]
Arrays.stream(matrix).flatMap(Arrays::stream).forEach(System.out::println);
```
### `skip`
Skips the first $n$ elements of the `stream`
```java
// [5, 6, 7, 8 ,9]
IntStream.range(0,10).skip(5);
```
### `limit`
Keeps the first $n$ elements of the `stream`
```java
// [0, 1, 2, 3, 4]
IntStream.range(0,10).limit(5);
```
### `distinct`
```java
IntStream.range(0,10).map(x -> x % 2 == 0 ? 0 : 1).distinct(); // [0, 1]
```
### `peek`
```java

```
### reduce
General-purpose reduction operation.
Always creates a new value from applying the accumulator on two values (and abandom them).
```java
IntStream.range(0, 10).reduce((x, y) -> x + y); // Optional - 45

// identity parameter
IntStream.range(0, 10).reduce(1, (x, y) -> x + y); // int - 46
```
### `anyMatch`, `allMatch`, `noneMatch`
```java
// true
IntStream.range(0,10).anyMatch(x -> x == 5);
// false
IntStream.range(0,10).allMatch(x -> x == 5);
// false
IntStream.range(0,10).noneMatch(x -> x == 5);
```
# Common terminal operations
### `toArray`
int[] array = IntStream.range(0,10).toArray();
### `collect`
```java
// `boxed()` method to convert the stream of primitives to a stream of their corresponding boxed objects.
List<Integer> list = IntStream.range(0,10).boxed().collect(Collectors.toList());
Set<Integer> set = IntStream.range(0,10).boxed().collect(Collectors.toSet());
Map<Integer, Integer> map = IntStream.range(0,10).boxed().collect(Collectors.toMap(i -> i, i -> i * i));
```
### `Join`

### Primitve value
```java
stream.max()/min()/count()/
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzOTE0Mzk3NjFdfQ==
-->