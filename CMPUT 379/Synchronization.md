#COMEBACKTOTHIS 
==Skipped missed a couple lectures==
# Concurrency
![[Pasted image 20231004120533.png]]
# Concurrent Processes
![[Pasted image 20231004120557.png]]
## Competing processes
- Processes that do not exchange information *cannot affect the execution of each other*, but they can *compete for devices and other resources*. Such processes do not intend to work together, and so are unaware of one another.
- **Example:** Independent processes running on a computer.
- **Properties**:
	- Deterministic.
	- Reproducible.
	- Can stop and restart without ‘‘side’’ effects.
	- Can proceed at arbitrary rate.
## Cooperating processes
- Processes that are *aware of each other, and directly (by exchanging messages) or indirectly (by sharing a common object) work together*, may affect the execution of each other.
- **Example:** Transaction processes in airline reservations
- **Properties**:
	- Share (or exchange) something: a common object (or a message).
	- Non-deterministic (a problem!).
	- May be irreproducible (a problem!).
	- Subject to race conditions (a problem!).
# Why Cooperation?
We allow processes to cooperate with each other, because we want to:
- Share some resources.
	- One checking account file, many tellers.
- Do things faster.
	- Read next block while processing current one.
	- Divide jobs into smaller pieces and execute them concurrently.
- Construct systems in modular fashion.
	- UNIX example:
```bash
cat infile | tr ‘[A-Z]‘ ‘[a-z]‘ |
sort | uniq –c | lpr
```
## Potential Problem
Instructions of cooperating processes can be **interleaved arbitrarily**. The order of (some) instructions are irrelevant. However, **certain instruction combinations must be eliminated**. For example:

| Process A  | Process B  | concurrent access |
| ---------- | ---------- | ----------------- |
| A = 1;     | B = 2;     | does not matter   |
| A = B + 1; | B = B * 2; | important!        |
A **race condition** is a situation where two or more processes access shared data concurrently and correctness depends on specific interleaving of operations (i.e. good luck).
## Mutual Exclusion 
- Mutual exclusion is a mechanism to ensure that *only one process (or person) is doing certain things at one time*, thus **avoid data inconsistency**. All *others should be prevented from modifying shared data* (i.e., the fridge or milk) until the current process finishes. 
- E.g., only one person buys milk at a time.
### Example
| time | Person A | Person B |
| ---- | -------- | -------- |
| 3:00 | Look in fridge. Out of milk. |                             |
| 3:05 | Leave for store.             |                             |
| 3:10 | Arrive at store.             | Look in fridge. Out of milk.|
| 3:15 | Buy milk.                    | Leave for store.|
| 3:20 | Leave the store.             | Arrive at store.|
| 3:25 | Arrive home, milk in fridge. | Buy milk.|
| 3:30 |                              | Leave the store.|
| 3:35 |                              | Arrive home. OOPS!|
- The ‘‘too-much-milk’’ example shows that when *cooperating processes are not synchronized, they may face unexpected ‘‘timing’’ errors*.
- What does correct mean? 
	- Someone goes to store to buy milk, but NOT everyone (too much milk!)
## Critical Section
- A **critical section** is a *section of code*, or a collection of operations, in *which only one process may be executing at a given time* and which we want to make ‘‘sort of’’ atomic. **Atomic** means *either an operation happens in its entirety or NOT at all*; i.e., it cannot be interrupted in the middle.
- E.g., buying milk.
- Atomic operations are used to ensure that cooperating processes execute correctly.
- [[#Mutual Exclusion]] mechanisms are used to solve the critical section problem.
![[Pasted image 20231004122730.png]]
## How to fix?
### Solution 1
- First attempt at computerized milk buying: leave a note:![[Pasted image 20231004122851.png|300]]
- This works for people because the first three lines are performed atomically; *but does not work otherwise*.
- ==This system is bad==
### Solution 2
- Second attempt: Use two notes: ![[Pasted image 20231004123104.png]]
- A leaves note, B leaves note, A sees B’s note, but does not yet remove A’s note, B sees A’s note, does not buy milk, A removes note and does not buy milk. B removes note and does not buy milk.
- ==Also bad, chance of no progress==
### Solution 3
- Third attempt: In case of tie, B will buy milk: ![[Pasted image 20231004123307.png]]
- This ‘‘asymmetric’’ solution works. *But is much too complicated*. The problem is that the mutual exclusion idea is simple-minded. Moreover, the code is asymmetric (and complex) and *process B is consuming CPU cycles while waiting*. In any case, the solution would be more complicated if extended to many processes (try to modify the code for four processes).
## Fundamental Requirements
Concurrent processes should meet the following requirements in order to cooperate correctly and efficiently using shared data:
1. **Mutual exclusion** - no two processes will simultaneously be inside the same [[#Critical Section]] *(CS)*.
2. **Progress** - a process wishing to enter its *CS* will eventually do so in finite time.
3. **Fault tolerance** - processes failing outside their *CS* should not interfere with others accessing the *CS*.
4. **No assumptions** - should be made about relative speeds or the number of processors. Must handle all possible interleavings.
5. **Efficiency** - a process will remain inside its *CS* for a short time only, without blocking.
- Also, a process in one *CS* should not block others entering a different *CS*.
# Mutual Exclusion Algorithms
## Attempt 1
`proc` is a global variable and initialized to A (or B). Both processes *start execution concurrently*.
![[Pasted image 20231006120605.png]]
- **Problem:** violates rule 2 (strict alternation).
	- Forces a "flip flop" between A and B, If A has to use critical section 20 times and B needs it only once, we are stuck waiting for B repeatedly.
## Attempt 2
The global variables `pAinside` and `pBinside` are initialized to `FALSE`.
![[Pasted image 20231006120711.png]]
- **Problem:** violates #1 (interleaved instructions). Both A & B can be in the critical section.
	- Once we pass the While loop in Process A (before `pAinside=TRUE;`), an interrupt can happen and once we return from the interrupt, We can restart in either process A or B. If we restart in process B, we Enter the while loop without problem and then both programs are in the critical section. 
## Attempt 3
The global variables `pAinside` and `pBinside` are renamed as `pAtrying` and `pBtrying`, respectively.
![[Pasted image 20231006120822.png]]
- **Problem:** violates rule #2 (progress).

## Dekker’s Algorithm 
If two processes attempt to enter a critical section at the same time, the algorithm will allow only one process in, based on whose turn it is. If one process is already in the critical section, the other process will busy-wait for the first process to exit. This is done by the use of two flags, `pAtrying` and `pBtrying`, which indicate an intention to enter the critical section on the part of processes A and B, respectively, and a variable turn that indicates who has priority between the two processes.
(Same as attempt 2 but with a check for the single bad case, kind of combines attempt 2 and 3)
![[Pasted image 20231006123019.png]]
- One more global variable, turn, initialized to A or B.
## Peterson’s Algorithm 
If A is in its critical section, then `pAtrying` is true. In addition, either `pBtrying` is false (meaning B has left its critical section), or `Turn` is A (meaning B is just now trying to enter the critical section, but graciously waiting), or B is trying to enter its critical section, after setting `pBtrying` to true but before setting `turn` to A and busy-waiting. So if both processes are in their critical sections then we conclude that the state must satisfy `pAtrying` and `pBtrying` being true, and `turn = A` and `turn = B`. No state can satisfy both `turn = A` and `turn = B`. 
![[Pasted image 20231006123243.png]]
Same global variables, but turn need not be initialized
(Note: the above relies on a race condition to resolve access rights, but it is not harmful).

## Both Dekker’s and Peterson’s algorithms are correct BUT
they only work for two processes. Similar to the last solution of the ‘‘too-much-milk’’ problem, these algorithms can be generalized for N processes, but:
- N must be fixed (known a priori), which is too much to expect.
- The algorithms become much too complicated and expensive.
==Implementing a mutual exclusion mechanism is difficult!==

## Bakery Algorithm 
Leslie Lamport envisioned a bakery with a numbering machine at its entrance so each customer is given a unique number. Numbers increase by one as customers enter the store. A global counter displays the number of the customer that is currently being served. All other customers must wait in a queue until the baker finishes serving the current customer and the next number is displayed. When the customer is done shopping and has disposed of his or her number, the clerk increments the number, allowing the next customer to be served. That customer must draw another number from the numbering machine in order to shop again. According to the analogy, the "customers" are threads, identified by the letter i, obtained from a global variable. Due to the limitations of computer architecture, some parts of Lamport’s analogy need slight modification. It is possible that more than one thread will get the same number n when they request it; this cannot be avoided. Therefore, it is assumed that the thread identifier i is also a priority. A lower value of i means a higher priority and threads with higher priority will enter the critical section first. 
![[Pasted image 20231006123602.png]]
![[Pasted image 20231006123614.png]]
# What’s Missing?
![[Pasted image 20231006124047.png]]
## A Simple-Minded Alternative
Let’s start by using hardware instructions to mask interrupts. If we don’t let the CPU interrupt (i.e., take away the control from) the current process, the solution for N processes would be as simple as:
![[Pasted image 20231006124119.png|400]]
Unfortunately, there is only one system-wide critical section active at a time. Besides, no OS allows user access to privileged instructions!
## Hardware Support
Many CPUs today provide **hardware instructions to read, modify, and store a word atomically**. Most common instructions with this capability are:
- TAS – test-and-set (Motorola 68K)
- CAS – compare-and-swap (IBM 370 and Motorola 68K)
- XCHG – exchange (x86)
- LL/SC – load-linked/store-conditional (MIPS, PowerPC)
The basic idea is to be able to *read out the contents of a variable (memory location), and set it to something else **all in one execution cycle***. Hence not interruptible. The use of these special instructions makes life easier!
## Yet Another Alternative!
![[Pasted image 20231006124333.png]]
- [p] Only one global guard variable is associated with each critical section (i.e., there can be many critical sections).
- [p] N processes; processes are unaware of N.
- [c] Busy waiting!

# Semaphores
A semaphore is a synchronization variable (guard) that takes on non-negative integer values with only **two atomic operations**:
![[Pasted image 20231013120500.png]]
Semaphores are simple, yet elegant, and allow the solution of many interesting problems. They are useful for more than just mutual exclusion.
- P causes program to wait until we can enter a critical section.
	- We wait until the semaphore is not zero (when it has been freed). We then allow access to critical section and then set it back to 0.
- V says "I'm done with the critical section"

## Semaphore Solution
Here is a solution of ‘‘too-much-milk’’ problem with semaphores:
![[Pasted image 20231013121330.png]]
Note: Semaphore `OKToBuyMilk` must initially be set to 1. Why?
- We have to actually enter the CS at the start

## Properties of Semaphores
Semaphores have several attractive properties:
- **Simple**.
- **Work with many processes** – single resource serialization.
- **Can have many different critical sections with different semaphores**.
- **Each critical section has unique access semaphore**.
- **Can permit multiple processes into the critical section at once, if desirable**—multiple (identical) resources.
	- If semaphore value is set to **more than 1** at the start, we can have more than one process in the critical section. (Think of multiple tellers at a store, we can have many people "checking out" at the same time and people in line waiting.)

However, they are unstructured and do not support data abstraction (see monitors). Unstructured => is a convention that relies on correct programming.
## Possible Uses of Semaphores
- **Mutual exclusion**.
	- Initialize the semaphore to one.
- **Synchronization of cooperating processes (signaling)**.
	- Initialize the semaphore to zero.
- **Managing multiple instances of a resource**.
	- Initialize the semaphore to the number of instances.
## Type of Semaphores
Semaphores are usually available in two flavors:
- **Binary** – integer value of 0 and 1.
- **Counting** – an integer value ranging between 0 and an arbitrarily large number. Its initial value might represent the number of units of the critical resources that are available. This form is also known as a **general semaphore**.
Note: this above definitions are correct for busy-wait semaphores. We will generalize this concept shortly.
## Implementation of Semaphores
No existing hardware implements P/Wait and V/Free operations directly. So, semaphores must be built up in software using some other elementary synchronization primitive(s) provided by hardware.
- **Uniprocessor solution:** can disable interrupts or use hardware support.
- **Multiprocessor solution:** harder! Possibilities:
	- Turn off access of all other processors (not practical!).
	- Use hardware support for atomic operations.
### Binary Semaphore – Busy-Wait
![[Pasted image 20231013123444.png]]
- Spinlock:
	- The process ‘‘spins’’ while waiting for the ‘‘lock’’.
	- Potential indefinite postponement.
	- Low efficiency (busy waiting).
- "Traps" a process in the waiting block loop until it is able to exit.
### Semaphore: Non-Busy Wait
![[Pasted image 20231013124058.png]]
- We create a queue so that we don't have a process that is "stuck" in a loop (wasting cycles). The queue is based on "arrival time" of the processes (like first come first serve).
- We shut the process down when it is in the `P` block if the CS is not available, the `V` block wakes up the next available proecess. 
- The Pseudo code does not work because
### Semaphores: Readers & Writers
- Allow one writer at a time, or many readers.
	- **For example**: Airline database. We do not want the customers to be able to read the flight times as they are being written because then they will be wrong or jumbled. 
- Initialize semaphores to…?
![[Pasted image 20231016120746.png]]
- We need to know how many people are reading
	- hence `readcount`
	- This is because we want to use a semaphore to stop the writer from writing (this is the `if` block)
	- *While any processes are reading. We cause the writer to wait. Once there is no readers happening, We free the writer and alow it to write.*
- 