A consistency model is used to establish some level of consistency across different runs of your programs. The common models form a hierarchy:

1. Strict Consistency: theoretical perfection.
2. Linearizability
3. Sequential Consistency: the result of any execution is the same as if the operations of all the cores had been executed in some sequential order.
	1. Equivalent to per-core program order being preserved + global total order
4. Causal Consistency

A single-core processor achieves SC by default. The fetch, decode, execute cycle happens strictly sequentially. Even with hardware optimizations like Out-of-Order execution or local store buffers, the CPU must ensure that the per-thread program order in preserved. This does not mean AT ALL that there aren't any [[Concurrency and Synchronization|race conditions]] during a multithreaded program! Even on a single-core processor, you can easily manufacture a situation where non-determinism and race conditions happen.

Multi-core processors (x86, at least), do not guarantee SC by default. They enforce a more relaxed model called Total Store Order. In this model, a core's loads can execute before its' stores become globally visible (to other cores). The defining principle is that **store->loads** are not ordered, but store->store, load->load, and load->store are.

The approach to achieving these levels of consistency is by enforcing [[Mutual Exclusion|mutual exclusion]]. A good mutual exclusion approach needs to have three things:
1. Mutual exclusion (of course)
2. Progress
3. Bounded waiting

