Every process has at least one thread to actually run it. A process is just a running program, and can be thought of as a resource container.

A short list of what a process contains:
- pid
-  A virtual memory heap (mapped to physical memory using paging and the mmu)
- text segment, where the code is stored
- .bss and .data for global/static uninitialized and initialized vars
- file descriptor table
- signal handler table
- list of TCBs, one per thread

A short list of what the threads inside processes contain:
- tid
- program counter/instruction pointer, where in the code the thread is currently executing
- register set, the architectural registers that the ISA exposes to the programmer (and aren't kernel managed), unlike microarchitectural registers like branch predictors and ROB
- stack
- signal mask
- scheduling state, whether the thread is running/ready/blocked, priority, niceness, affinity
