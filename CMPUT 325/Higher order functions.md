- Takes other functions as input OR
- Produces function as output

- Often used to separate computation patterns from specific action
	- eg. iterate over a list and "do something" for each element

# Some Typical Higher Order Functions
- Map
- Reduce
- Filter
- Vector
## Map
- Apply a function to each element in list
- collect all results in list
- eg. salary raise
	- input: payroll, AND function implementing raise
	- output: new payroll with increased salaries 
	- ![[Pasted image 20250123101748.png]]
	- ![[Pasted image 20250123101835.png]]
> [!important]
> In the raise function, we need to write `(inc car(L))` as the helper function, but the rest of `raise` just applies `inc` to the entire list, we can generalize `raise` as `map(f, L)` to deal with this instead

![[Pasted image 20250123102158.png]]
