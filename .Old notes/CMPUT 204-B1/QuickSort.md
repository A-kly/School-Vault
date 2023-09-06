uses [[Divide-and-Conquer]]
![[Pasted image 20230213102740.png]]
```pseudo
procedure QuickSort(A,p,r)
	**sorts the subarray A[p,...,r]
	
	if (p < r) then 
		q <- Partition(A,p,r)
		**Partition returns q such that
		** (i) A[q] = pivot
		** (ii) All elements <= pivot appear in A[p,...,q-1]
		** (iii) All elements > pivot appear in A[q+1,...,r]
	QuickSort(A,p,q-1)
	QuickSort(A,q+1,r)
```
_Finds a pivot for the array, quick sorts everything above and below the pivot using the value of the pivot, calls on each half recursively_
- Using extra arrays costs us extra space and is inefficient, we should try to sort _in place_


```pseudo
procedure Partition(A,p,r)
	
	pivot <- A[r]
	i <- p - 1
		for (j from p to r-1) do
			if (A[j] <= pivot) then
				i <- i+1
				exchange A[i] <-> A[r]
			exchange A[i+1] <-> A[r]
		return i+1
```
![[Pasted image 20230213101845.png]]
_Does the actual sorting of the subarrays, spits out a pivot value such that:__
- `A[q]` = pivot
- All elements <= pivot appear in `A[p,...,q-1]`
- All elements > pivot appear in `A[q+1,...,r]`
_All elements before and after pivot are_ **not sorted** _but are simply less than and greater than respectively_
_Recursive calls make all subarrays sorted_


# Correctness
![[Pasted image 20230213101913.png]]

# Analysis
![[Pasted image 20230213102410.png]]
Recursion Tree:
![[Pasted image 20230213102430.png]]
# RT Analysis
==**# KC = Number of Key comparisons**==
![[Pasted image 20230213103128.png]]
**Loot at and understand T(n)**: _Definition of recurrence relation. 
One key compare from (pivot vs every other key). 
T(n1) comparisons for front subarray. 
T(n-1-n1) comparisons from second subarray._
## Worst case
![[Pasted image 20230213103415.png]]
![[Pasted image 20230213103521.png]]
![[Pasted image 20230213103545.png]]
_Case 2 has an error, 8 and 1 should be swapped_
