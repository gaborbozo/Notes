# Processes
* Foreground processes
* Daemons which are running continuously as a background process and wakes up to handle periodic service requests, which often come from remote processes
## Create end termination
## Create
* System initialization
* Process resulting system call
	* copy of the original (fork)
	* replacement of the original (execve)
	* ...
* User request
* Batch tasks
### Terminating
#### Voluntary
* exit
* return
* exception
### Involunatry
* illegal operation
* external instruction
## Process tree
A process has **a parent** and can have **multiple children**
## Process Condition
* running
* ready to run
* blocked
### State transitions
* running -> blocked
* running -> ready to run
* ready to run -> running
* blocked -> ready to run
## Shared memory
A way for different programs to communicate and pass data without more overhead from communications processes
### Access time degradation 
When several processors try to access the same memory location it causes contention
### Lack of data coherence
Whenever one cache is updated with information that may be used by other processors, the change needs to be reflected to the other processors, otherwise the different processors will be working with incoherent data
## Mutual exclusion
A **mutex** (mutual exclusion object) is a program object that is created so that multiple program thread can take turns sharing the same resource
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzODEwNjIxNDBdfQ==
-->