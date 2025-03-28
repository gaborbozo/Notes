# Java
Java is a **C**-based, **strongly typed** language - Almost every expression and subexpression type is known at compile time. **Dynamic binding** - Calls classes recursively during runtime in a way defined by the compiler.

The **Java Virtual Machine (JVM)** translates Java programs into bytecode. The **Java Runtime Environment (JRE)** includes the **JVM** and additional libraries. It provides a connection between the program and the operating system. The **Java Development Kit (JDK)** includes the **JRE** and development environments.
# Program Structure
Hierarchical namespace The directory structure must reflect the package structure, as both the compiler and the virtual machine can only perform dynamic linking if these match. It is also important to run the program from the correct directory.
## Qualified Name Resolution
### Import
At the compilation unit level, we can refer more easily to classes - we resolve the class path and can refer to its name throughout the program. **Not transitive**, meaning that if, for example, `import java.util.*`, it imports all the binaries of the `utils` package, but not the contents of other packages within it. In case of a **name collision**, the compiler notifies, and in such cases, there is **no import** - the full path must be written out.
### Static Import
Refers not to a class but to a class's static field/method. `import static java.util.Arrays.sort`
## Jar Files
Compressed masses of **.class** files.
# Javac
## Javac Switches
`-d <directory>` Target directory for compiled files (**Out Of Tree Build** - "do not mess with the source files").

`--source-path <path>, -sourcepath <path>` Path to access not yet compiled files (source codes).

`--class-path <path>, -classpath <path>, -cp <path>` Path to already compiled files. `-encoding <encode>` Setting character encoding.

# Javadoc
## Javadoc Parameters
```java
/**
Sets the hour property. Pass {@code hour} satisfying {@code 0 <= hour && hour <= 23}
@param hour The value to be set
@throws IllegalArgumentException If the supplied value is not between 0 and 23 inclusively
*/
public void setHour(int hour)

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzg1NjI5OTUzXX0=
-->