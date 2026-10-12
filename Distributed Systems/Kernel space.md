The kernel space is not some monolithic program, but event-driven and lives in every process space. It is shared by all processes: all of these pages map onto the exact same frames in RAM. Why? so that no context switching ever has to happen during syscalls.

- The actual kernel code, of course
- Process tree
	- PCBs
		- Register state (PC, IP, etc)
		- Scheduler info (process priority, time quantums)
		- fd table (includes devices, files, pipes, sockets, etc)
- Open file table
- Kernel managed buffers: pipes/sockets

All of the above are on the kernel heap.

From the perspective of a user space process, this memory is protected. In order to "access" the kernel space, it must be done through a couple of special methods:

System calls (synchronous) - MSRs
- The processor transfers control to a kernel entry point via special registers.
Interrupts - IDT
- Hardware (async, from external devices)
- Software (synchronous)
Exceptions (synchronous) - IDT
- Traps
- Faults