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
### Why Cooperation?
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
### Potential Problem
Instructions of cooperating processes can be **interleaved arbitrarily**. The order of (some) instructions are irrelevant. However, **certain instruction combinations must be eliminated**. For example:

| Process A  | Process B  | concurrent access |
| ---------- | ---------- | ----------------- |
| A = 1;     | B = 2;     | does not matter   |
| A = B + 1; | B = B * 2; | important!        |
A **race condition** is a situation where two or more processes access shared data concurrently and correctness depends on specific interleaving of operations (i.e. good luck).
#### Example
| time  | Person A | Person B |
| 3:00  | Look in fridge. Out of milk. | Look in fridge. Out of milk. |
| 3:05  | Leave for store. | Leave for store. |
| 3:10  | Arrive at store. | Arrive at store. |
| 3:15  | Buy milk. | Buy milk. |
| 3:20  | Leave the store. | Leave the store. |
| 3:25  | Arrive home, milk in fridge. | Arrive home. OOPS! |
| 3:30 | 
| 3:35 | 



Leave for store.
Arrive at store.
Buy milk.
Leave the store.
Arrive home. OOPS!