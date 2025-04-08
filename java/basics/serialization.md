# Serialization
Converting object into byte stream.
1. Retrieve the fully qualified class nem of the object,
2. Retrieve the object's _serialVersionUID_,
3. Check if the class metadata in the metaspace to get information about the class structure,
4. Write the object's class descriptor (_name_, _serialVersionUID_) and the actual object data to the output stream.

Serializable objects need to implement the `java.io.Serializable` or its subinterface `java.io.Exernalizable`.
# Deserialization
Converting byte stream into object.
1. JVM reads the class descriptor (_name_, _serialVersionUID_) from the stream,
2. It check the metasapce to see if the class already loaded, if not then it tries to find it;
   * if found, it verifies that the _serialVersionUID_ matches the serialized object's _serialVersionUID_,
   * if not found, a _ClassNotFoundException_ is thrown,
4.  The JVM then reconstructs the object using the default constructor or by bypassing it if `readObject()` is overridden.
# Security implications
- If an attacker injects a malicious serialized object and the JVM loads an unexpected class, it can lead to **Remote Code Execution (RCE)**.
- Deserialization may trigger loading of unexpected classes if the application improperly handles class resolution.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzk5OTIxODk0XX0=
-->