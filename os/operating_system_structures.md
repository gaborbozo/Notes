# Operating system structures
## Monolithic Approach
Very basic operating system in which file management, memory management, device management, and process management are directly controlled within the kernel
## Layered Approach
0. Processor assignment and multiprogramming
1. Memory management
2. Machine operator process
3. Input/Output management
4. User application programes
5. Machine operator
## Micro-kernels
This structure designs the operating system by removing all non-essential components from the kernel and implementing them as system and user programs. This result in a smaller kernel called the micro-kernel
## Virtualization
The operating system achieves virtualization with the help of a specialized software called a **hypervisor**, which emulates the PC client or server CPU, memory, hard disk, network and other hardware resources completely, enabling virtual machines to share resources

VMWare, MS Virtual Server, Virtual PC

Hyper-V, XEN-KVM, VMWARE
<!--stackedit_data:
eyJoaXN0b3J5IjpbODMxMTUzNDJdfQ==
-->