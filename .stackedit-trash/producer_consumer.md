# Producer and consumer
There are two processes that need to synchronize with each other at certain intervals and may exchange data.

We refer to the point in time when the two processes need to communicate as a **rendezvous**, ideally allowing each process to proceed without waiting for the other.
## Intermediate Data Structure
The overly fast consumer may be forced to wait, while the producer may occasionally get ahead. As a result, the uneven production over time needs to be balanced.

To achieve this, implementing an intermediate data structure is necessary for proper functioning.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzY3OTAxNTAwXX0=
-->