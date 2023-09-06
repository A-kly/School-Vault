How many Units of time are used?
- Often we run into exponential time
- We want polynomial or linear time
How do we measure it?
- Can be boiled down to it's bare minimum with [[Asymptotic Growth of Functions]]

Must be:
- Hardware independent
- compiler independent
So:
- Create abstract model
- Identify "Key operations": If each one costs me one unit, how many units does it take for my procedure?
	- Primitive operations take 1 time unit;
		- Assignment operations
		- calling a method/function
		- arithmetic operations
		- comparisons
		- returns
	- Loops take # times executed
	- Mem accesses are instant

How do we count?
eg. [[Insertion Sort]]:
```pseudo
procedure InsertionSort(A) **sort A[1...n] 
	for j = 2 to n do ** from 2 -> n+1 (n Times)
		key = A[j] **insert A[j] into sorted sublist A[1 ... j-1]  (n-1 Times)
		i = j-1 ** (n-1 Times)
		while (i>0 and A[i]>key) do **(sum all from j=2 to n of tj )
			A[i+1] = A[i] ** (sum all from j=2 to n of tj-1)
			i = i-1 ** (sum all from j=2 to n of tj-1)
		A[i+1] = key ** (n-1 times)
```
![[Pasted image 20230111104536.png]]
- do _for_ test n times
	- everything in for loop happens n-1 times
	- do _while_ test an arbitrary number of times (say tj) for all n-1 loops of the _for_ loop
		- everything in _while_ loop happens ![[Pasted image 20230113101308.png]] times
			- everything in _while_ loop happens an arbitrary number of times (minus one from extra _while_ compare) for every (n-1) loop of the _for_ loop, every arbitrary _for_ loop time is added together

# RT Analysis in different cases
Worst case:
- T(n) -- maximum time over all input size n (upper bound)
Average case:
- Must specify input distribution over which average is computed
- Most common: assume **uniform distribution** (all inputs of size n equally likely)
Best case:
- Least running time for any instance; useful only for lower bound

# RT Analysis of Insertion sort
Best Case:
- List is already sorted (for any 2 <= j <= n we have tj=1)
	- $$T(n) = 2n-1+3(n-1)=5n-4$$
Worst Case:
- list is in reverse sorted order (for any 2 <= j <= n we have tj=j)
	- $$T(n)=2n-1+3[(n(n+1)/2)-1]=1.5n^2 + 3.5n -4$$
Average Case:
- Suppose we randomly chose n numbers and apply InsertionSort. On average, half of the elements in `A[1..j]` are less than `A[j]` and half are greater. So tj is about j/2 and we and up with a quadratic function, as bad as worst case.

# Summary

_Random access machine_: Ideal model of RT analysis computation.
- What operations your computer can do in a single instruction with one unit of cost
_Pseudo code_: standardized model of describing algorithms
_Insertion sort example_: RT analysis, worst, best, average case

