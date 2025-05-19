# Streams
`Collections` are a group of related classes and interfaces that represent data structures such as lists, sets, and maps.
`Streams` allows us to process collections of elements in a **functional** and **declarative** way.

There If the order of the the iteration does not matter, then the items can be **consumed parallel**.

`Stream` is an abstraction which focuses on the all insted of the parts.
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
```java
.filter();

.peek();

.map();
.flatMap();

.skip();
.limit();

.distinct();

.sorted();
```
## Utilization - back to concrete  - **terminal** operations
```java
.forEach();

// Transforming
.collect();

// Concatenated as a String
.join();

// Converting into a single result
.count();
.sum();
.max();
.min();

.reduce();

// Logical operations
.anyMatch();
.allMatch();
.noneMatch();
```
# Parallel Streams
At a certain point different threads pick up the work and on another point they will wait for each other before continuing. 

Two options to create:
* `.parallelStream()` instead of `stream()`,
* or use the `.parallel()` method on a `Stream`.

```java
// Without parallel it will return 16
// With parallel it may return 16 or more because of multiple threads
Stream.of(1, 2, 3, 4, 5)
//.parallel()
.reduce(1, (x, y) -> x + y);
```

Running something parallel not inherently means that it is faster. The work needs to be split up, merged and memory managed.
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTExODkyNDcyLC0xMzkxNDM5NzYxXX0=
-->