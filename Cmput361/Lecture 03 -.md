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
- 