InsertionSort 
    - RT Analysis: Worst-Case; Average; Best
    - Input: n elements (a'1, a'2, ....., a'n) where each pair is comparable
    - Output: an ordered permutation of the n elements such that a'1 ≤ a'2 ≤ ....., ≤ a'n ( non decending order)
    - Our first solution: Insertion sort
        - Idea: repeatedly insert A[j] into sorted sublist ` A[1 ... j-1]` 
        - How to insert? One by one move elements into sorted sublist ` A[1 ... j-1]`which are bigger than ` key (= A[j]) `to the right
    - ` Sort it: [6,5,3,1,4,8]` 
    - ` j=2 >> indexing starts at 2` 
    - ` key = 5 >> current element to be sorted` 
    - ` 6 is coppied into 2nd position`
    - ` i = j-1 >> i loops through until key is less than left neighbor`
    - 
    - ` [6,5,3,1,4,8] j=2 key=5` 
    - ` [6,6,3,1,4,8] ` 
    - ` [5,6,3,1,4,8] j=3 key=3`
    - ` [5,5,3,1,4,8]`


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
