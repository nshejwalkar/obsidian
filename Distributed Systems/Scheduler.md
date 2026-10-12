Different scheduling algorithms exist to schedule processes/threads onto the physical cores. Threads are scheduled for a maximum of the time quantum: for example, Windows has one of around 100-120ms. 

First come first serve
Shortest Job First
Round Robin
Fixed Priority
Earliest Deadline First
Completely Fair Scheduler (Linux default)
Multilevel Feedback Queue + RR/FIFO for same priority (Mac default)

Various problems arise because of the way these tasks are scheduled.

Convoy effect
Lock Holder Preemption
Priority inversion
