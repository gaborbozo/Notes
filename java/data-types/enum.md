# Enum
Enumeration type in Java is a type of data structure that allows to define a set of named constants, represents a fix set of values that do nat change during the lifetime of a program.
These values actually are objects which were created at compiling time.

Type-safe way to define a fixed set of constants that represent different options.
```java
enum Day {SUN, MON, TUE, WED, THU, FRI, SAT}
```

It is reference type so instances can be made of it . 
```java
Day fav = Day.SAT; //explicit referencing
fav = 3; //implicit referencing - buildtime error
```
These objects can not be instanced but manually can create constructors which will be called when refering to the enum value
```java
enum Coin{
	PENNY(1),DIME(10);

	private int value;

	Coin(int value){
		this.value = value;
	}

	public int getValue(){
		return value;
	}
}
```
```java
Coin coin = Coint.Penny;
coin.getValue();
```
Equality checks can be made by using `==` or `equals()`. Since each enumeration type is an object these equlity checks are performed by comparing the references to the objects, rather than their values
```java
enum Day { MONDAY, TUESDAY, WEDNESDAY }
Day  myDay  = Day.MONDAY;
if (myDay == Day.MONDAY) //true
if (myDay.equals(Day.MONDAY) //true
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDA2NTA5NzQ4XX0=
-->