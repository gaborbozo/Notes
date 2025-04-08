# Memory in java
Stack memory cleaned automatically.
Heap memory cleaned by the JVM.
# Garbage collector
It is an automatic memory management system that identifies and removes unused objects to free up memory
## Counter strategy (old)
Counts references to an object; when it reaches zero, the object is deleted. The problem with this approach is that we can have cyclic references.
## Marking and sweeping strategy
Marks reachable objects and sweeps away unreferenced ones.
#### Normal sweeping
Deletes unreferenced objects leaving gaps between still referencing ones. Prone to cause _Out of Memory Error_.
#### Sweeping with compacting
Deletes unreferenced objects and rearrange remaining ones to avoid empty gaps. Problem with it is that it has an extra _fragmentation_ operation.
#### Sweeping with copying
Instead of rearranging remaining ones, all of them are copied to another memory space and the one was used is deleted entirely.
### Heap generations
In heap there is **young an old generations/tenured space**, while non-heap memory is called **metaspace**.

Java's idea about objects is that they don't live too long.

In young generation objects are created in the so called **eden space**. When a certain treshold is reached the garbage collection starts and moves objects that are still alive to the **survivor space**, cleaning up the eden space using _sweeping with copying_. When a treshold is reached again, objects which are in the survivor space are taken to the **old generation** meaning that if the object is still referenced, then it may be there for a while.

Freeing up memory in the old generation can be very costful. For easier creating the **metaspace** contains klass structure, methods of classes, constants, annotations and optimizations in order to create more easier new object of the given type.

When the _metaspace_ size grows beyond the threshold of the VM, it will try to free up memory first, or when it runs into a metaspace out of memory, it will try to fix it by running garbage collection on it.
# Garbage collectors
Java has 5 built-in GCs, and each one is an improved version of another.
## Serial GC
Young generation: mark and copy.
Old generation: mark sweep compact.
Running on a single thread.
Stop-the-world implementation - the rest of the application is frozen until the gc has done a full cycle.
## Parallel GC
Young generation: mark and copy.
Old generation: mark sweep compact.
Running on multiple threads.
Stop-the-world implementation.
## Concurrent Mark Sweep (CMS) GC
Young generation: mark and copy, stop-the-world.
Old generation: mark sweep compact and mostly concurrent.
Running on multiple threads.
Stop-the-world and mostly concurrent.
## Garbage-First (G1) GC
Divide heap into small regions.
Keeps track of amount of live and dead objects.
Aims for shortest pauses possible.
Running on multiple threads.
Concurrent and stop-the-world processes.
## Z GC
Aims for max 10ms pauses.
Reference coloring instead of using a map
# JVM Tuning
Selecting the most suitable garbage collector implementation may be the last step of optimizing the performance of Java applications. It's is not necessary when the
* memory functioning all right,
* latency is all right,
* is the **throughput** (the amount of work that can be done with chosen units of time, hight means that the application may need more memory) normal.
## Heap size and relation to GC
Smaller heap means that GC needs to happen more often, but when the heap is too large, a full GC cycle can take very long. Best heap size depends on the application, less than 5% of the execution time should be garbage collecting.
# Memory leaks
Keeping objects that are no longer needed.
* avoid string concats, builders instead,
* close resources such as streams and connections,
* overrite `equals` and `hashCode` in order to differ the objects being errased.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk3OTM0OTgwM119
-->