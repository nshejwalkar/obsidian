the problem (1999): How do we create 10000 concurrent client connections on our server? the problem was originally introduced for client connections, but exposed a lot of common i/o problems that could be extrapolated to general tasks.

before, architectures would spawn a new kernel thread for every new connection. remember, each kernel thread requires its own kernel stack (8mb virtual, but only a few 4kb pages at minimum). not actually the problem, though, scheduling and constant context switching are.

dpdk solves this
netflix solves this