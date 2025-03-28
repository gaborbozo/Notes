# JDBC and JPA Overall
## JDBC
Java Database Connectivity is the JavaSoft specification of a standard API that allows Java programs to access database management systems
Consists of a set of interfaces and classes

Helps with
* Connecting to a data source
* Sending queries and update statements to the database
* Retrive and process the results received from the database
## JPA
Java Persistence API is a specification that gives some functionality and standard to ORM tools. It is used to examine, control, and persist data between Java objects and relational databases
## JDBC vs JPA
JDBC requires differenct scripts must be written for different databases, while JPA is database-agonistic, meaning that the same code can be used in a variety of databases 

JPA-based applications still use JDBC under the hood meaning that JPA is another abstraction layer that hides lower-level JDBC calls
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgzNzMzOTM4Ml19
-->