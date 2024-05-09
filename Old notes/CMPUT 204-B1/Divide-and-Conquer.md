Uses the [[Divide-and-Conquer]] methodology

If [[Recursion]] is used, running time is a bit hard to figure out but uses [[Divide-and-Conquer]].

**For Merge Sort**:
- Recursively divide input until we reach small input
```pseudo
Merge(A;lo,mid,hi)
	B <- A[lo,mid]      **linear time (B and C are both sorted already)
	C <- A[mid+1, hi]   **linear time
	result <- new empty list
	while (both B and C are non-empty)     **key comaprisons
		if (head(B) < head(C)):            **simple operations
			Append head(B) to result
			Remove head(B) from B
		else:                              **simple operations
			Append head(C) to result
			Remove head(C) from C
	Append all remaining elements in (B) to result
	Append all remaining elements in (C) to result
	A <- result    **A is stored
	Return A
```
![[Pasted image 20230130101143.png|300]]![[Pasted image 20230130101931.png|300]]
_We need n-1 key comparisons. We compare the heads of each subarray once accept for the last subarray (in the diagram above, number 8) as it just gets appended to the end._
![[Pasted image 20230130101801.png]]
_`nB` is the number of inputs in the subarray B and `nC` is the number of inputs in the subarray C_

## High level idea:

>Splitting the input list in half, sorting each half list, and then merging them back into a single list, roughly half as long as sorting the original input list

Questions:
1. Q1: why not splitting the list into fourths or eighths?
2. can we do the splitting infinitely-many times?
3. Really half as long?


## Smaller recursive pseudo code

```pseudo
Merge-Sort(A;lo,hi)
	if (lo < hi) then
		mid = FLOOR((lo + hi)/2)   **(1)
		Merge-Sort(A;lo,mid)       **(2)
		Merge-Sort(A;mid+1,hi)
		Merge-Sort(A;low,mid,hi)   **(3)
```
	(1) Break the list in half unless it is an empty or single- element list (divide part)
	(2) Recursively sort the two sublist 
	(3) Merge the two sublist into a single list (Conquer part)

![[Pasted image 20230130102702.png|600]]
Blue: DIVIDE PART
Red: CONQUER PART

## Two parts
```
if (lo < hi) then
	mid = FLOOR((lo + hi)/2)
	Merge-Sort(A;lo,mid)
	Merge-Sort(A;mid+1,hi)
```
_Recursively break the list in half_: Θ(1)
_Why? Easy operation to do the breakdown, linear time_
And then:
```
Merge-Sort(A;low,mid,hi)
```
_Merge the two sublist into one_: Θ(n)
_Why? Each layer takes `n-1` key comparisons where n is the input size in each sublist.__
`n-1 ∈ Θ(n)` 

## Overall running time

T(n) = running time
![[Pasted image 20230130103648.png]]
`T(n) = T(n/2) + T(n/2) + n-1`
_This is called a recurrence relation because the running time is defined by itself_

## Recurrence Relations
![[Pasted image 20230130104136.png|600]]

## Solving Recurrences
### Method #1: Iterated Substitutions

Simple example:
![[Pasted image 20230130104234.png]]
Generally:
![[Pasted image 20230130104247.png]]
![[Pasted image 20230130104302.png]]

#### For [[Divide-and-Conquer]]:
![[Pasted image 20230130104523.png]]
![[Pasted image 20230130104618.png]]
