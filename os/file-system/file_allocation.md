# File allocation
## Contiguous allocation
### First fit
In this method, first job claims the first available memory with space more than or equal to it’s size
| Advantages | Disadvantages |
|--|--|
| Fast in processing | Can waste a lot of memory |
### Best fit
In this method, the operating system first searches the whole of the memory according to the size of the given job and allocates it to the closest-fitting free partition in the memory
| Advantages | Disadvantages |
|--|--|
| Memory Efficient | Slow in processing |
### Worst fit
the process traverses the whole memory and always search for the largest hole/partition, and then the process is placed in that hole/partition
| Advantages | Disadvantages |
|--|--|
| It will leave a large internal fragmentation for other processes | Slow in process |
## Linked(Chained) allocation
The file data is in a chained block list
| Advantages | Disadvantages |
|--|--|
| No data loose | Slow process, especially the last item |
## Index file allocation
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTE5MTc4Mjk1XX0=
-->