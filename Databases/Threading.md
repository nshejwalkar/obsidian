There are different types and levels of threads.

At the bottom are **hardware threads**, which are decoupled from the number of physical cores when we consider physically new silicon for special CPUs like Intel's Hyper-Threading and AMD's SMT.
- duplicates the registers and the program counter to be twice that of the number of cores.

The OS is agnostic-ish (see [[Better Schedulers]]) of whether hyper-threading or not is implemented for the hardware. it spawns **kernel-level threads** (or just threads, because 1:1 is most common) which are scheduled by the scheduler onto these hardware threads. for example, if Linux spawns 1000 threads and the CPU has 4 cores x 2 hyperthreads = 8 hardware threads, the Linux scheduler must schedule these 1000 to timeshare on those 8 threads.

**User threads** live purely in user space and are extremely cheap. Are only an application level concept, the OS does not know about these.

Unlike the mapping from kernel-level threads to hardware "threads," the threading model to map user-space threads to kernel-level threads has evolved over time.
- 1:1 Model
- N:1 Model
	- [[C10k problem]]
- N:M Model

https://0xkiire.com/mn-concurrency-model/