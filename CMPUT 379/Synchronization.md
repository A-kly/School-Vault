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
```