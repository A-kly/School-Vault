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
# Mutual Exclusion
## Attempt 1
`proc` is a global variable and initialized to A (or B). Both processes *start execution concurrently*.
![[Pasted image 20231006120605.png]]
- **Problem:** violates rule 2 (strict alternation).
	- Forces a "flip flop" between A and B, If A has to use critical section 20 times and B needs it only once, we are stuck waiting for B repeatedly.
## Attempt 2
The global variables `pAinside` and `pBinside` are initialized to `FALSE`.
![[Pasted image 20231006120711.png]]
- **Problem:** violates #1 (interleaved instructions). Both A & B can be in the critical section.
## Attempt 3
The global variables `pAinside` and `pBinside` are renamed as `pAtrying` and `pBtrying`, respectively.
![[Pasted image 20231006120822.png]]
- **Problem:** violates rule #2 (progress).