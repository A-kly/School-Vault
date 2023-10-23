# What Is a Deadlock?
Deadlock is defined as the *permanent blocking* of a set of processes that compete for system resources, including database records or communication lines. 
Unlike other problems in multiprogramming systems, there is *no efficient solution to the deadlock problem in the general case*. 
**Deadlock prevention, by design, is the "best" solution**. 
Deadlock occurs when a set of processes are in a wait state, because each process is waiting for a resource that is held by some other waiting process. **Therefore, all deadlocks involve conflicting resource needs by two or more processes**.
# Classification of Resources
Two general categories of resources can be distinguished:
- **Reusable:** something that can be safely used by one process at a time and is not depleted by that use. Processes obtain resources that they later *release for reuse by others*. 
	- E.g., CPU, memory, specific I/O devices, or files.
- **Consumable:** these can be created and destroyed. When a resource is acquired by a process, the *resource ceases to exist*. 
	- E.g., interrupts, signals, or messages.
Another taxonomy dimension again identifies two types of resources:
- **Preemptable:** these can be *taken away from the process owning it with no ill effects* (needs save/restore).
	- E.g., CPU.
- **Non-preemptable:** *cannot be taken away* from its current owner without causing the computation to fail. 
	- E.g., printer.

==Deadlocks occur when sharing reusable and non-preemptable resources.==
# Conditions for Deadlock
