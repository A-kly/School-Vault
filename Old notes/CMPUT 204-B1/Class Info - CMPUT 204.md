
- Instance: One unit of an algorithm
- Algorithm: steps to get from A to B
- What do we care about in algorithms?
    - Correctness
    - Amount of resources (Space/time complexity)
    - Can we do better?
- [[Recursion|Recursive Algorithms]]
    - The factorial function:
        - n! (insert math def here)
        - recursive implementation:

```
def factorial(n)
	if (n=0) then 
		return 1 //base case
	else
		return n * factorial(n-1) //recursive call 
```


- looks like induction (assume base case holds, prove k+1)
- how do we prove this is correct?
	- Claim: for every natural number n, factorial(n) = n!
	- proof by induction:
		- (Base case) We show that the claim holds for some initial value
			- For n=0 we have 0! = 1 and factorial(0)=1
		- (Ind step) Assume factorial(k) = k! (ind hypothesis)
			- factorial(k+1) = (k+1) * factorial(k) = k+1 * k!  //by ind hypothesis = (k+1)! 
	- else block of code = sub-problem (ind hypotheses) is solved correctly
	- if block = induction hypothesis

Pseudocode:
    - "Input: integers a, b"
    - "output: a x b"
    - Conventions:
        - Indentation for block structure
        - while/for/repeat/if/then/else
        - "procedure" or "function" to create a function
        - **"****" or ">>" for comment
        - array indexing: A[i] for the i'th cell of array A
            - **Arrays start at 1** 

- Concluding remarks:
    - Prove my claim holds for **ALL** base cases
        - Strong induction = many sub-problems