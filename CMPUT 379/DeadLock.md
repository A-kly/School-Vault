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
## … A Knot Is Required
Cycle is a *necessary condition* for a deadlock. But when dealing with multiple unit resources, **not sufficient**.
A **knot** must exist—**a cycle with no non-cycle outgoing path from any involved node**.
- At the moment assume that:
	- A process halts as soon as it waits for one resource, and
	- Processes can wait for only one resource at a time.
## Further Requests
![[Pasted image 20231025120628.png]]
# Strategies for deadlocks
In general, four strategies are used for dealing with deadlocks:
- **Ignore:** stick your head in the sand and *pretend there is no problem at all*.
- **Prevent:** *design a system in such a way that the possibility of deadlock is excluded* a priori (e.g., compile-time/statically, by design)
- **Avoid:** *make a decision dynamically* checking whether the request will, if granted, potentially lead to a deadlock or not (e.g., run-time/dynamically, before it happens)
- **Detect:** let the deadlock occur and detect when it happens, and *take some action to recover after the fact* (e.g., run-time/dynamically, after it happens)
# Theory Versus Practice
Different people react to this strategy in different ways:
- **Mathematicians:** find deadlock totally unacceptable, and say that it *must be prevented at all costs*.
- **Engineers:** ask *how serious it is*, and do not want to pay a penalty in performance and convenience.
The *UNIX approach is just to ignore the problem* on the assumption that most users would prefer an occasional deadlock, to a rule restricting user access to only one resource at a time. 
The problem is that the ==prevention price is high==, mostly in terms of putting inconvenient restrictions on processes.
# Deadlock Prevention
The strategy of deadlock prevention is to design a system in such a way that the *possibility of deadlock is excluded a priori*. Methods for preventing deadlock are of two classes:
- **indirect methods** prevent the occurrence of one of the necessary *conditions listed earlier* -> [[#Conditions for Deadlock]].
- **direct methods** prevent the occurrence of a *circular wait condition*.
Deadlock prevention strategies are very conservative; they solve the problem of deadlock by limiting access to resources and by imposing restrictions on processes.
## More on Deadlock Prevention
- **Mutual exclusion**
	- In general, this condition ==cannot== be disallowed.
- **Hold-and-wait**
	- The hold and-wait condition can be prevented by *requiring that a process request all its required resources at one time, and blocking the process until all requests can be granted simultaneously*.
- **No preemption**
	- One solution is that *if a process holding certain resources is denied a further request, that process must release its unused resources and request them again*, together with the additional resource.
- **Circular Wait**
	- The circular wait condition can be prevented by *defining a linear ordering of resource types (e.g. Directed Acyclic Graph). If a process has been allocated resources of type R, then it may subsequently request only those resources of types following R in the ordering*.

# Deadlock Avoidance
Deadlock avoidance, allows the necessary conditions but makes judicious choices to ensure that a deadlock-free system remains free from deadlock. With deadlock avoidance, *a decision is made dynamically* whether the current resource allocation request will, if granted, potentially lead to a deadlock. Deadlock avoidance thus requires knowledge of future requests for process resources.
- Ways to avoid deadlock by careful resource allocation:
- Resource trajectories.
- Safe/unsafe states.
- [[#Dijkstra’s Banker's algorithm]].
## Dijkstra’s Banker's algorithm
### Definitions
![[Pasted image 20231025121608.png]]
### Resource request
![[Pasted image 20231025121629.png]]
### isSafe
![[Pasted image 20231025121644.png]]
### what is safe?
![[Pasted image 20231025121700.png]]
