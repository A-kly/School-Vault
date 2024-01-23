# Boolean queries
## EBNF definition
- term stands for a single term in vocab
```python
query = term |
	(query) |
	query :and: query |
	query :or: query |
	:not: query;
```
- and, or and not are Boolean values
## Computing answers with bit vector operators
- each row is a term doc incidence matrix
- bitwise operators on each vector