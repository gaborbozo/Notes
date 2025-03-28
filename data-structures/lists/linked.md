# Linked Lists
**Advantage**: Sorted insertion/deletion does not require moving elements.

**Disadvantage**: Cannot be indexed with constant time complexity, only with $O(n)$!
## Singly Linked List
`key, next` attributes  
`search`, `insert`, `delete`
### Simple Singly Linked List (S1L)
For traversal, typically start with `pe=0, p=L` pointers.  
At the end of iterations, it’s worth checking if `pe=0` remained.
### Headed Singly Linked List (H1L)
**S1L** + the first value corresponds to a null value.  
For traversal, typically start with `pe=L, p=L->next` pointers.  
At the end of iterations, it’s worth checking if `pe` remained as the head element.
### Headed Singly Circular Linked List (C1L)
**H1L** + the last element points to the head element.  
For traversal, typically start with `pe=L, p=L->next` pointers.  
Check until `p != head element`.
## Doubly Linked List
`key, prev, next` attributes  
`precede(q, r)` - Insert `q` before `r`.  
`follow(q, r)` - Insert `q` after `r`.  
`unlink(q)` - Delete `q`.
### Simple Doubly Linked List (S2L)

### Headed Doubly Linked List (H2L)

### Headed Doubly Circular Linked List (C2L)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUyODQ3NzE5XX0=
-->