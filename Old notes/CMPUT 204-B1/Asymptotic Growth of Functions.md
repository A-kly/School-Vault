# Recap: How fast is [[Insertion Sort]]?

![[Pasted image 20230120102755.png]]
# Asymptotic Notation
Asymptotic = "In the limit"

![[Pasted image 20230120103249.png|400]]
 _[[Big-O|Big O notation]]_: 
- O(f(n))
- "Big O of f(n)"
- Region 1 + Region 2 ("≤")

 _[[Big-Ω|Big Omega notation]]_:
- Ω(f(n))
- "Big Omega of f(n)"
- Region 1 + Region 3 ("≥")

 _[[Big-Θ|Big Theta notation]]_: 
- Θ(f(n))
- "Big Theta of f(n)"
- Region 1 ("=")

==Θ(f(n)) = O(f(n)) ∩ Ω(f(n))==


### ***What is the point of C and n0?*** #review

- _c_ scales f(n), this means that for any c, f(n) is scaled by c to show that it is cf(n) is always upper bounded by O(n), lower bounded by Ω(n) and, with an extra c1, grows at the same rate as Θ(n)

- _n0_ is a positive constant that indicates the minimum size of the input size, O(n), Ω(n) and Θ(n) only works for input of sufficient size

## Overview
![[Pasted image 20230123104349.png]]

## Little-o and Little-ω

![[Pasted image 20230123104810.png]]

## Tips 
![[Pasted image 20230125102804.png]]

## Logarithms 

![[Pasted image 20230127101434.png]]
Tips:
![[Pasted image 20230127101848.png]]
![[Pasted image 20230127102503.png]]
![[Pasted image 20230127103016.png]]
(_Why are these even important?? Like there are hella slides on it but it seems mostly irrelevant to how we will be graded????_)
![[Pasted image 20230127103143.png]]

## Concluding remarks

1. [[Big-O]] is **NOT** just for worst case!
	- Big-O with worst case input gives us *an upper bound for the entire algorithm*

2. _I need to develop an intuitive understanding of some common Big-O notations:_
	- Polynomials: `n^k` (`k` is a constant) Examples:
		- `n`
		- `n^2`
		- `sqrt(n)`
	- Logarithms
		- `log(n)`
	- Exponents: `a^n` (`a` is a constant) Examples:
		- `2^n`
		- `e^n`
	- Combinations of above:
		- `n log(n)`
		- `log(log(n))`

3. Ignore Everything that happens at LOW _n_ values
	- ![[Pasted image 20230127103958.png|400]]

# NOTE: ==I have stopped taking general notes for this class as I believe it would be much more beneficial to just add the content that I'll have a hard time understanding. ==

Summary: