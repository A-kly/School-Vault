# Limitations of Boolean retrieval
## Boolean queries
Pros:
- [p] Easy to understand.
- [p] Explainable.
- [p] Easy to implement.
- [p] Suitable for expert users
Cons:
- [c] Hard to "get right" (misplaced :or: or :not: can lead to disaster).
- [c] Does not recognize that some terms are more important than others.
- [c] Documents are either "in" or "out".
	- [c] No notion of "partial answer".

## The feast or famine nature of Boolean queries
![[Pasted image 20240130125405.png]]
![[Pasted image 20240130130014.png]]
# Not all terms are equally important
## Rare terms/phrases are more important
![[Pasted image 20240130130402.png]]
# Ranked Retrieval
![[Pasted image 20240130130839.png]]
## Desirable properties of a good scoring function
![[Pasted image 20240130131323.png]]
![[Pasted image 20240130132256.png]]
![[Pasted image 20240130132304.png]]
### How well does the Jaccard coefficient meet our criteria?
![[Pasted image 20240130132323.png]]
# Documents as vectors and scoring with dot products
## RECAP: The term-document incidence matrix
![[Pasted image 20240130132609.png]]
![[Pasted image 20240130132741.png]]
## The bag-of-words model
![[Pasted image 20240130132751.png]]
![[Pasted image 20240130132822.png]]
![[Pasted image 20240130132939.png]]
# The tf-idf family of weights
