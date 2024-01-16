# Search Engines and Term-Document Incidence Matrix
- Our goal today is to understand how documents (and queries) are pre-processed by the IR system
	- What are documents? What are the choices? Does it matter?
	- How is the content of the documents (and queries) processed?
	- What are the "terms"? What are the choices? Does it matter?
- **Question: why do we have aquarium in the matrix even if some documents have Aquariums ?**
	- The matrix term is in the singular and in lower case.
	- ![[Pasted image 20240116123627.png|300]]
# Documents
## What is a document (from lecture 1)
![[Lecture 01 - Foundations#Documents]]
## Why does it matter?
- Reason #1 -- scoring
	- Number of words can affect scoring of document
	- terms rare in whole book may be common on certain page of book
- Reason #2 -- showing results to users
- 