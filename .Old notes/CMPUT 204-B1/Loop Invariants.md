# Concepts 
## [[Insertion Sort]]: Correctness

```pseudo
function InsertionSort(A) **sort A[1...n]

	for j = 2 to n do
		key = A[j] **insert A[j] into sorted sublist A[1 ... j-1]
		i = j-1
		while (i>0 and A[i]>key) do 
			A[i+1] = A[i]
			i = i-1
		A[i+1] = key
```
What does a loop do? What is cumulative effect? Does it do what it's supposed to do?

## For simple programs, use logic:
Example:
```pseudo
procedure Swap(a,b)

temp <- a
a <- b
b <- temp
```
_Claim_: for any two pointers ___a___ and ___b___, the function assigns value at b to a and the value at a to b.
_Proof_: (trace it out with a diagram) ![[Pasted image 20230116101529.png]]

## Terminology
- A _Loop-invariant_ is an ==assertion about the state of the code== that is ==always true== at the ==beginning of each loop iteration==

## Steps to prove program correctness:
kind of like proving [[Recursion]]
1. Identify loop invariant
	1. Do I understand what the code does?
	2. Do I understand the cumulative effect of the loop?
	3. Can I word exactly the cumulative effect?
2. Prove the loop invariant for:
	1. Initialization (like base case of induction)
	2. Maintenance (like induction step of regular induction)
	3. Termination #1: Does the loop halt eventually? (Not in induction)
	4. Termination #2: How do I prove the correctness of the Loop-invariant?
![[Pasted image 20230118100702.png]]

# Example #1 (FindSum)

```pseudo
procedure FindSum(A,n)

sum <- A[1]
while (j =< n)
	sum <- sum + A[j]
	j <- j+1
return sum
```
- First Loop iteration begins at j=2
- _"At the beginning of an iteration"_ : the first line of the loop
- At the beginning of an iteration, what holds true, so that its being true throughout implies the correctness of the procedure? (pre step to step 1)
	- when `j = 2`, `sum = A[1]`
	- when `j = 3` , `sum = A[1] + A[2]`
	-  when `j = k` , for any `k < n`, `sum = A[1] + ... + A[k-1]`

Step 1: Identify loop invariants:
- "At the beginning of each loop iteration `(j)`, `sum = A[1] + ... + A[j-1]`"
	- **Must be rigorous and correct**
		- "At the beginning of each loop iteration `(j)`, `sum = A[1] + ... + A[j]`" - ***WRONG***

Step 2: Prove the loop invariant for all properties

- Initialization: Does it hold before the loop starts?
	- Before the loop begins, `sum = A[1] = A[1,...,(2-1)]`
- Maintenance: If it holds for j-th iteration, does it hold for the j+1-th iteration?
	- Suppose for the j-th iteration, `sum = A[1] + ... + A[j-1]`
	- Then at the beginning of iteration j+1, `sum_after = sum_before + A[new_j - 1]`
		- `new_j = j + 1`
- Termination #1 : Does the loop end?
	- The loop ends when we eventually increment j to >n
- Termination #2: When the loop ends, does it lead to the correctness of the overall algorithm/claim we are making?
	- When the loop terminates, `j = n + 1`, in which case the LI implies `sum = A[1] + ... + A[j-1]`

# Example #3:
```pseudo
procedure FindMax(A,n)

m <- A[1]
for (i from 2 to n)
	if A[i] > m then
		m <- A[i]
return m
```
For each iteration:
> `i = 2, m = A[1]
> `i = 3, m = max{A[1], A[2]}`
> `i = 4, m = max{A[1], A[2], A[3]}`
> . . .
> `i = n, m = max{A[1], ..., A[n-1]}`

Loop invariant: FindMax returns the largest element in the array A 
	At the beginning of iteration i, `m = max{A[j] : 1 =< j =< i}`



# Difficult example, induction proof:

```pseudo
Procedure fib3(n)

if n==0 then 
	return 0

x <- 0; y <- 1
for j = 2 to n do
	newy <- x+y
	x <- y
	y <- newsx
return y
```

- Loop Invariant:
	- At the beginning of iteration `j >= 2`,
	- `x = Fib(j-2)`
	- `y = Fib(j-1)`
- Proof:
	- Initialization: At the start of first iterations when `j = 2`:
		- `x = fib3(j-2) = fib3(0) = 0`
		- `y = fib3(j-1) = 1`
	- Maintenance: Assume L.I. holds for iteration `j >= 2`. We show that L.I. holds at the start of next iteration `j + 1`.
		- `newy_new = x_old + y_old` by the code
		- `newy_new = Fib(j-2) + Fib(j-1)` by induction hypothesis (L.I.)
		- `x_new = y_old = Fib(j-1)` by the code
		- `y_new = newy_new = Fib(j-2) + Fib(j-1) = Fib(j)`
		- `j_new (restart loop) = j + 1`
		- Therefore,
		- `x_new = Fib(j - 1) = Fib(j_new - 2)` L.I. Holds!
		- `y_new = Fib(j) = Fib(j_new - 1)` L.I. Holds
	- Termination #1: `j` Increases by 1 every iteration, eventually reaching `n + 1`. 
	- Termination #2: When the loop terminates, `j = n+1`, then it follows that:
		- `y = Fib(j-1) = Fib(n)`

## Difficult example: Correctness Proof
This procedure contains two Loop Invariants for [[Insertion Sort]]

_Top down approach_: assume inner loop works and prove outer, then prove inner
_Bottom up approach_: Prove inner loop and then outer loop

## Top down:

```pseudo
function InsertionSort(A) **sort A[1...n]
	for j = 2 to n do
		key = A[j] **insert A[j] into sorted sublist A[1 ... j-1]
		i = j-1
		####################
		##Assume this works#
		####################
		A[i+1] = key
```

Loop invariant (For-Loop):
	"At the beginning of the for loop iteration `j`, `A[1,...,j-1]` contains the same elements that were there initially, only in order."

```pseudo
function InsertionSort(A) **sort A[1...n]
	######################################
		########Assume this works#########
		##################################
		while (i>0 and A[i]>key) do 
			A[i+1] = A[i]
			i = i-1
		##################################
```
Loop invariant (While-Loop):
	"Let `A_before = [1...j]` denote the arraybefore we started itterating through the while loop. The at the beginning of each iteration of the while loop:
	1. `A[1..i+1] = A_before[1..i+1]`
	2. `A[i+2..j] = A_before[i+1..j-1]`"

