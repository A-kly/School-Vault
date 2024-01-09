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
### Terms
- Terms are *unique tokens* among indexed documents