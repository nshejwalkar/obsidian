A process is a running program in user space. When the kernel (also a running program, but not considered a process) creates a new process, it adds it to the PCB and gives it an address space (visual below). The actual virtual memory addresses of these pieces in the space are randomized on process creation by ASLR.

![[Pasted image 20261010222136.png]]

The process is given an amount of virtual memory depending on the process architecture (whether the program was compiled to handle 32 or 64 bit memory addresses), the OS architecture (same thing for the kernel; it'll force the cpu to run in that mode) and the cpu architecture (the size of its word). 32-bit => 2^32 = 4GB virtual memory. 

Important parts
- [[Kernel space]]: the entire kernel! inaccessible by user code
	- when a syscall happens, there's a hardware interrupt -> trap into the kernel = IP moves to this part of the process (so no context switching)
- Stack (grows downward)
- mmap (where dynamic libraries are loaded in, like iostream)
- heap (grows upward)
- BSS
- Data
- Text

Processes are completely isolated from each other, the only form of communication being [[Inter-Process Communication]]. If you want to have concurrent/logically separate workers without the problems of context switching overhead and IPC, use threads (see [[Processes vs Threads]]).

Processes can be in various states. How do we know which processes to schedule on the cores, from ready->running? The [[Scheduler]] handles that. 

![[Pasted image 20261011190535.png]]