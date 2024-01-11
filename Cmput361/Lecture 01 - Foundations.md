# Why do we search?
Common tasks for web search engines:
- search for products/services, aka. business transactions
- search for reading materials of interest
- searching for answers to a specific question
**Note**: input to a search engine is called a query #definition
## Transactional queries
We know what we want and are trying to find it.
- **General web search engine** is mostly used
	- This is because of google adds and shit. Systems in place for it
	- Search engines can provide personalized results
## Informational queries
We don't know what we are looking for and we search documents for the answers. Answers are long and found in these documents
- We can use a **General web search engine** or a **specialized web search engine** (like ualberta library)
## Question answering
We want to answer a question where we don't know or are unsure of the answer. Answers are short, verifiable and very specific (one correct answer).
- Use a **general web search engine**, they are good because they have *knowledge graphs* consisting of info found on pages
- systems like ChatGPT can answer some questions correctly
## Other places where search engines are used
- Personal search (on your own computer, spotlight)
- Enterprise search (within an organization only)
- Vertical search (Across the web but about specific topics, eg. yelp)
# Documents, queries, tokens & terms
## Documents
- Storage and retrieval unit of a search system
	- system always returns documents or links to documents
- Examples:
	- Gmail returns links to emails (doc = email)
	- Yelp returns business profiles that it keeps (doc = business profiles)
	- Library returns book records (doc = book records)
When making search engine, you decide what documents are
## Queries
- Input to search engine
- Search interface can have multiple fields (beartracks), or single box (google)
- query is an **expression of the info needed by user**
- Types:
	- Keyword (self explanitory)
	- Phrase (uses "" in google)
	- Wildcard (uses * , regular expressions)
## Tokens
- *internal representation* of words appearing in documents and queries
- **tokenization** is the process of converting words in queries/documents to tokens.
	- eg, converts all of: "Hello", "hello", "hellO" to "hello"
	- "hello" is token
### Terms
- Terms are *unique tokens* among indexed documents.
- All terms are the **vocabulary of the system**.
- A query token that does appear in any document is called **out-of-vocabulary** (OOV)
	- system just discards that word
### Why tokenize?
- help users find documents that have words that are slightly different from words in documents
- removes inconsistencies across documents
- examples:
	- case folding (Edmonton -> edmonton)
	- removing punctuation (U.S.A -> USA)
	- Acronym expansion (AFN -> Assembly of First Nations)
# Architecture of a Search Engine
## At the highest level
- Documents added to an *index* and ordanized based on *terms*.
- documents can be deleted
- Users send queries and receive results through search interface
- engine matches *tokens* in *query* to *terms* in index to get documents with most of *query tokens*
![[Pasted image 20240109134542.png|600]]
## What will be covered in 361?
- How to tokenize documents and queries.
- How to represent documents.
- Different kinds of indexes, for different kinds of queries.
- Suitable data structures for representing indexes.
- Different methods for matching documents and queries.
## What about Web Search Engines?
- Main difference is that documents are found by *web crawlers* that continuously crawl
- engine has no control over quality of documents so it must be careful to avoid attacks and exploitation
- There is a separate index for terms -> advertisements
![[Pasted image 20240111125422.png|600]]
# Representing documents
## Term-Document incidence matrix
![[Pasted image 20240111125505.png|600]]
- We match terms to documents using a term-document incidence matrix
- This provides mapping of terms to documents
- the matrix keeps weights (`wij`) indicating the importance of 