Mutual exclusion can be enforced at different levels of abstraction.

- Software level
	- Peterson's algorithm
	- Hoare Monitors
	- Brinch-Hansen monitors
- OS level
	- Sleep/wake
	- Semaphores
	- Mutexes
	- Message-passing primitives
- Hardware level
	- Disabling interrupts
	- Special instructions (CLI/STI, test-and-set)

We want to apply these solutions around a "critical section" where it's imperative that we don't get interrupted.
#### Hardware
###### asm volatile cli, sti
This has the effect of preventing preemption of the process by the kernel. When the APIC sends its interrupt to the CPU core, the core ignores it because cli clears the interrupt flag. But this only applies to that single core, not other threads on other cores. It also only really works in kernel mode anyway, and is completely inflexible.

#### Software
##### shared variables
doesn't work. Without special instructions or anything, threads can deadlock by both setting then both checking.
##### Peterson's algorithm
For two threads, 
##### Lamport's Bakery Algorithm
For multiple threads