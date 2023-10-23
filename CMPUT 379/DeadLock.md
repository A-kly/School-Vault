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
Four conditions that must hold for a deadlock to occur:
1. **Mutual exclusion:** processes require exclusive control of its resources (not sharing).
2. **Hold and wait:** process may wait for a resource while holding others.
3. **No preemption:** process will not give up a resource until it is finished with it.
4. **Circular wait:** each process in the chain holds a resource requested by another.
# Real-World Example
![[Pasted image 20231023123111.png]]
## My Example
![[Pasted image 20231023123158.png]]
# Discussion
If any one of the necessary conditions is prevented a deadlock need not occur. For example:
- Systems with only simultaneously shared resources cannot deadlock.
	- *Negates mutual exclusion*.
- Systems that abort processes which request a resource that is in use.
	- *Negates hold and wait*.
- Preemptions may be possible if a process does not use its resources until it has acquired all it needs.
	- *Negates no preemption*.
- Transaction processing systems provide checkpoints so that processes may back out of a transaction.
	- *Negates irreversible process*.
- Systems that prevent, detect, or avoid cycles.
	- *Negates circular wait. Often, the preferred solution*.

# Resource Allocation Graphs
![[Pasted image 20231023124642.png]]

## Cycle Is Necessary, But ...
![[Pasted image 20231023125149.png]]
