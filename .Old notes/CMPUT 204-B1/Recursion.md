
- Fibbonacci Numbers 
    - n = 0 : F(n) = 0
    - n = 1: F(n) = 1
    - n > 1: F(n) = F(n-1) + F(n-2)
    - 
    - recursion is almost a copy of the definition
        - This means that we unfortunately create a tree representation of it
        - ![[Pasted image 20230109143724.png]]

```python
procedure fib1(n) 
if n<2 then
	return n
else
	return fib1(n-1) + fib1(n-2)
```

- Fibonacci Numbers 
    - n = 0 : F(n) = 0
    - n = 1: F(n) = 1
    - n > 1: F(n) = F(n-1) + F(n-2)
    - 
    - recursion is almost a copy of the definition
        - This means that we unfortunately create a tree representation of it
	- ![[Pasted image 20230109143748.png]]
```python
procedure fib1(n)
if n<2 then
	return n
else
	return fib1(n-1) + fib1(n-2)
```

- How many recursive calls?
	- Each call produces 2 more calls to fib1
	- Can be considered constant time
	- for fib1(4):
		- fib1(n-1) ‒ 1 time
		- fib1(n-2) ‒ 2 time
		- fib1(n-3) ‒ 3 time
		- fib1(n-4) ‒ 5 time
		- fib1(n-5) ‒ 8 time
		- **These values correspond to fib numbers** 
	- Claim: for all natural numbes n≥2, fib1(n-i) is invoked F(i+1) times for any 1 <= i <= n-1.
- How many recursive calls?
	- Each call produces 2 more calls to fib1
	- Can be considered constant time
	- for fib1(4):
		- fib1(n-1) ‒ 1 time
		- fib1(n-2) ‒ 2 time
		- fib1(n-3) ‒ 3 time
		- fib1(n-4) ‒ 5 time
		- fib1(n-5) ‒ 8 time
		- **These values correspond to fib numbers** 
	- Claim: for all natural numbes n≥2, fib1(n-i) is invoked F(i+1) times for any 1≤ i ≤ n-1.

# Recursive algorithm

- Running time = $$=\big{(}\frac{(1+\sqrt5)}2\big{)}^2$$
- Non recursive implementation
```pseudo
procedure fib2(n)

F[1]=0
F[2]=1
for j=3 to n+1 do 
	F[j] = F[j-1] + F[j-2]
return F[n+1]
```
- What did we do?
	- took the recursive definition and broke it down
	- Recursive:
		- Read from left to right :
		- If answer not defined (n>=3); evaluate until we know the answer
			- Many redundant calls
	- Non recursive 1:
		- Read from Right to left:
		- Define all answers up until the one we need
		- No redundant calls

- Non recursive Implementation 2:
```pseudo
procedure fib3(n)

if n=0
	return 0
x = 0
y = 1
for j = 2 to n do 
	newY = x+y
	x = y
	y = newY
return y
```
- Same as Non recursive 1 __without saving result__

# Induction
Strong Induction
Ind step: Fix some n. number k

FOR ALL 1 =< i **<** k, assume p(i) (our claim) and prove p(**k**)
assuming base case is n=1

OR

FOR ALL 1 =< i **=<** k, assume p(i) (our claim) and prove p(**k +1**)
assuming base case is n=1
