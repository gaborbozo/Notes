# Unit testing
Isolate written code to test and determine if it works as intended.
It only tests one thing at a time.
* Arrange - setup phase
* Act - action phase
* Assert - asserting unit tests
## Test coverage
A function can have multiple outcome. Test coverage measures the extent of possible outcomes.
```java
...

if (number < 50)
	...
if (number < 150)
	...
if (number < 250)
	...
	
...
```
Because coverage has a connection with possible outcomes this function should be tested atleast $4$ times
## Asserts
* `assertEquals`
* `assertSame`
* `assertTrue`
* `assertNul`
* `assertArrayEquals`
* `assertIterableEquals`
* `assertLinesMatch`
* `assertTimeout,assertTimeoutPreemptively`

Almost every function has it's negate: `assertNotEquals,assertFalse`...
## Catching errors
#### assertThrows
```java
@Test 
void testException(){ 
	assertThrows(IllegalArgumentException.class, () -> { 
		// Code that should throw an IllegalArgumentException
		throw new IllegalArgumentException("Invalid argument");
	});
}
```
#### assertDoesNotThrow
```java
@Test
void testNoException() {
	assertDoesNotThrow(() -> {
		// Code that should not throw any exception
		int result = 1 + 2;
     });
}
```
## Parametrized
Able to run the same test logic with different values representing different scenarios.

```java
@ParameterizedTest
@ValueSource(ints = {1, 3, 5, 7, 9})
void isOddNumber(int number){
	assertTrue(number % 2 != 0);
}
```
```java
@ParametrizedTest
@CsvSource({
"1,2,3",
"4,5,6",
"7,8,9"
})
void test(int a, int b,int c)
```
```java
@ParametrizedTest
@CsvSource(textBlock = """
   1,2,3
     4,5,6
    7,8,9
   """)

//first row have zero spaces
//second has two 
//third has one
```
## Grouping assertions
Multiple assertions in a single logical assertion block ensuring that all assertions within the block are executed, even if some of them failed. It allows all the assertion failures at once insted of stopping at the first failure.
```java
@Test
void testMultipleAssertions(){
	assertAll("numbers",
		() -> assertEquals(2, 1 + 1),
		() -> assertEquals(4, 2 * 2),
		() -> assertEquals(6, 3 + 3)
	);
}
```
# Mocking
A mock is a **fake class** that can be examined after the test is finished for its interactions with the class under test.

Mock Testing provides the ability to isolate and **test your code without any interference of the dependencies and other variables like network issues and traffic fluctuations**. In simple words, in mock testing, **we replace the dependent objects with mock objects**

**Mocks** are used to create fully mock or dummy objects, When it's called mock simply creates **a bare-bones shell instance** of the Class.
**Spies** are used for creating **partial or half mock objects**. In case it's created it will wrap an existing instance of the given object which will behave in the same way as the normal instance

**Without mocking or spying** an object we will get `NotAMockException`
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMDcyNjQyOTddfQ==
-->