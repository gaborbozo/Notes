## DTO validation
`jakarta.validation`
1. `Size, Min, Max, NotNull, etc.` annotated on the dto's properties
2. On a function's argument add the `@Valid` keyword (`public void func(@Valid Type object)`)
## Globally handled exceptions
Instead of defining an `@ExceptionHandler` on a controller, a better practice may be to define a
```java
@ControllerAdvice
public class ExceptionHandler extends ResponseEntityExceptionHandler { ... }
```
to gain controll over the most general error cases in Spring boot.


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI1NTM1NTc0NywxNjMyMTYyNDQyXX0=
-->