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
	- size of doc matters to user
	- page of book or whole book?

## How are documents encoded?
- Documents are digital files... the IR system must be able to read them.
	- Ex: this is what a digital (hexadecimal) "file" looks like:
```
4469676974616C20646F63756D656E74732074686174206172652074686520696E70757420746F20616E20696E646578696E672070726F6365737320617265207479706963616C6C7920627974657320696E20612066696C65206F72206F6E206120776562207365727665722E205468652066697273742073746570206F662070726F63657373696E6720697320746F20636F6E76657274207468697320627974652073657175656E636520696E746F2061206C696E6561722073657175656E6365206F6620636861726163746572732E20466F72207468652063617365206F6620706C61696E20456E676C697368207465787420696E20415343494920656E636F64696E672C2074686973206973207472697669616C2E20427574206F6674656E207468696E677320676574206D756368206D6F726520636F6D706C65782E
```
- What words are in it?
- What language is it in?
- IR systems need to know that! 
	- Assuming that the previous "file" was encoded in UTF-8, its content would be:
```
Digital documents that are the input to an indexing process are typically
bytes in a file or on a web server. The first step of processing is to convertthis byte sequence into a linear sequence of characters. For the case of plainEnglish text in ASCII encoding, this is trivial. But often things getmuch more complex.
```
- What if the system did not know that the encoding was UTF-8?
	- we guess encoding
		- try several, look for valid/real words
## Metadata
- Files come with metadata
- It tells us the language and encoding of the document
- Well built websites using good tools will provide this info to crawlers
- not always the case
- Http header example:
	- ![[Pasted image 20240116124732.png]]
## File formats
- formats can have more info that the text we see
### Example: Html tags
- Keep? remove? do we care about boldness or format of text in results? 
- **IT DEPENDS**
![[Pasted image 20240116124915.png]]
#### why do we care?
- Scoring
	- If doc 1 has token in <\title>, then it is more likely to be a good result than doc 2 where it is only in body
	- doc 1 may be more specific on topic
- Metadata search
	- Sometimes we are interested in the author of a document or the date when the document was written, instead of the words inside that document. HTML meta tags can be useful in such cases.
### DOCX format
![[Pasted image 20240116125305.png|600]]
#### A paragraph inside a DOCX file
```xml
<w:p>
<w:pPr>
<w:pStyle> w:val#"MyStyle"/>
<w:spacing w:before#"120" w:after#"120"/>
</w:pPr>
<w:r>
<w:t xml"space#"preserve">A paragraph is main container in a
document that further consists of a one or more runs where
the text of paragraph is actually contained.</w:t>
</w:r>
</w:p>
```
- Do we keep the `<w:p>` , `<w:pPr>` tags in our IR system or not?
	- It depends on the application! 

### File format nightmare -- PDF
> "Each PDF (Portable Document Format) file encapsulates a complete description of a fixed-layout flat document, including the text, fonts, vector graphics, raster images and other information needed to display it." (from https://en.wikipedia.org/wiki/PDF)

> Text in PDF is represented by text elements in page content streams. A text element specifies that characters should be drawn at certain positions. The characters are specified using the encoding of a selected font resource.

- It is possible to have a separate text element for each character in the document! “Spaces” are not explicitly represented; we can’t tell where words start or end!

## Take home message
- Digital files are just **long strings of bytes**.
- The encoding system allows us to **map groups of bytes into characters**.
	- Some encodings using up to four bytes for a single character.
- **High-quality web servers provide the encoding used for each file**.
- Search engines need to **guess the encoding** when it is not provided.
- The **file format specifies how the characters and words are displayed**.
	- Sometimes we care about that, but other times we do not.
	- It depends on the application.
# Words, Tokens, and Terms
- A **word** is a *delimited string of characters* as it appears in the content of the document (or the user query).
- A term is a unique **normalized** word (case, morphology, spelling, etc).
	- Different words can be normalized into the same term: a term defines an ==equivalence class of words==.
	- The **tokenizer** is a tool that defines how words are normalized into terms.
- A token is an instance of a term in the document (or query). 
![[Pasted image 20240116130712.png]]
## Finding words
- word = delimited sequence of characters
	- English: blank spaces and punctuation are delimiters
- **Compound words**?
	- *open* - seperated by spaces ("search engine")
	- *closed* - no spaces ("airport")
	- *Hyphenated* - Using hyphens ("one-of-a-kind")
	- Compound words are more than just words put together!
		- They have their own meaning
### Example: Finding words in Chinese
- We can write in Chinese without whitespaces
	- This can cause problems with meaning
- Some Chinese words can have multiple meaning depending on context
	- This ALSO causes problems
- Japanese also has these conserns
### Long compound words
Eg. 
- Compound noun in German: Lebensversicherungsgesellschaftsangestellter
	- leben (life)
	- versicherung (insurance)
	- gesellschaft (company)
	- angestellter (employee)
- **Should we break that down into four tokens?**
	- Keep full phrase and index it?
	- also break it down and index it?
	- do both?
	- show the best results! (long word is more rare, rank those results higher)
- Similar examples in many other languages: Dutch, Swedish, Turkish, Nunavut Inuktitut...
### Typical CMPUT361 exam question (SIMILLAR TO ON EXAM)
> Recall that in some languages, like German, some phrases are spelled by concatenating words into a single, and potentially very long, compound word. Explain the benefits and the drawbacks of a tokenizer that splits a long compound word into the constituent words and then normalizes each of them.
- Benefits:
- [p] More results for partial query match
- Drawbacks:
- [c] more tokens will have to be parsed in the query
## Bidirectionality
- Arabic is read "right-to-left", except when we run into Arabic numerals!
- ![[Pasted image 20240116131606.png]]
- The UTF encoding system resolves this issue.

## Diacritics
- A **Diacritic** is a *glyph added to a base letter* (or to another glyph).
- Eg. *acute*, *grave*, and *circumflex accents*
- Some languages have dozens of diacritics
### What do we do with them?
- Option #1 -- keep them!
	- Modern encoding has codes for all of them, keep them in docs and queries
- Option #2 -- remove them!
	- simple, 
- **Overall: do what we expect users to do when writing queries!**
	- ![[Pasted image 20240116132320.png]]
## Normalization
### What is it?
- Transforming text into **canonical** form.
	- The only, "true" form of a word
- **multiple transformations often used**
- **same transformations used for documents and queries**
### Why?
- Used to find matches when user writes word with different spelling
	- Ex: query mentions fish bowl and document mentions Fish Bowls (different capitalization and use of plural).
### Typical normalization steps
![[Pasted image 20240116133008.png]]
![[Pasted image 20240116133025.png]]
### Normalizing dates and numbers
- **Dates:** 3 ways (in the Gregorian calendar): `3/20/91`, `20/3/91` , `Mar 20, 1991`
- **Phone numbers:** `7804922285` or `(780) 492-2285` ?
- **Numbers:** some countries use `.` as decimal separator while others use `,` !
- **Money:** is `$1M` the same as `$1,000,000` ?
- A good system will normalize all of these to one canonical structure
## Take home message
- **Tokenization** is the process of *finding words, breaking them down into tokens* (e.g. think about compound words) and normalizing the tokens.
- Recall that before tokenization we need to *deal with the file format* (e.g., decide if we keep or remove HTML tags, or decode PDF content streams).
- Finding words and breaking them into tokens is *highly language dependent*.
- English is an easy language to deal with compared to most.
- We also tokenize and **normalize numbers, dates, emojis, hashtags, slang, acronyms**, ...
- There is no right or wrong, really. We do what the users find useful.
# Lemmatization and Stemming (Normalization based on Linguistic principles.)
## Lemmas and Stems
- Previous normalizations were based on heuristics. 
- Lemmatization and Stemming are based on **Linguistics**.

- **Lemma** is a word that stands at the *head of a definition in a dictionary*.
	- Least marked form of a word
	- For **Nouns**: Singular form (mouse instead of mice)
	- For **Verbs**: infinitive form (go instead of went)
- A **Stem** is the part of the word that never changes even when *Morphologically inflected*.
	- example: the stem of "produced" is "procuc" because:
		- Produces
		- producing
		- etc.
## Lemmatization
- **Lemmatization**: Do a proper reduction of the word to headword form, reserving *inflections* done to word
- **Inflections:** change word because of grammar, (tense, plural, voice)
- Examples of *lemmatization*:
	- ![[Pasted image 20240116134933.png|300]]
### Derivation and inflection are different things
- **Derivation:** create new words from other ones
	- Changes part of speach of the word we start with
	- ![[Pasted image 20240118123459.png|400]]
#### How is that different from inflection?
- **Derivation** creates a *new lemma*! **Inflection** creates a *word with the same lemma*.
## Stemming
- **Stemming:** "crude heuristic" that *removes the suffixes* in the hope of achieving similar effects of lemmatization
	- In principle, we could also remove prefixes -- but most stemmers do not do that.
- Simple example:
	- If a word ends in s , remove it. The intent here is to revert words from plural to singular.
	- Situation where it *works:* cats → cat
	- Situation where it *doesn't:* access → acces
- **The problem with heuristics is that there are always many corner cases to address.**
![[Pasted image 20240118131327.png]]

### The Porter stemmer
- Most well known and most used stemmer
- 5 steps, each with several rules:
- **deals with plurals and the -ed suffix**
	- ![[Pasted image 20240118125908.png]]
#### Guarded rules
- Only apply under some conditions
- Don't wanna destroy the word too much, leading to meaningless content.
![[Pasted image 20240118130310.png]]
![[Pasted image 20240118130613.png]]
## Lemmatization vs stemming
- **Lemmatization**:
	- "Reverses inflection".
	- Always produces a word (that can be found in the dictionary).
	- Requires deep linguistic knowledge.
	- Preserves the concepts in the user query.
- **Stemming**:
	- Is fast, and does not require look-up on dictionaries or other resources.
	- Is crude and does not distinguish inflection from derivation.
- **Both are known to increase recall**.
## Code
You are encouraged to use NLTK (https://www.nltk.org/) for lemmatization and stemming.
	Stemming: https://www.nltk.org/howto/stem.html
	Lemmatization: https://www.nltk.org/api/nltk.stem.wordnet.html#module-nltk.stem.wordnet
NLTK is a well-supported and established toolkit for Natural Language Processing in Python.

You may also use Spacy (https://spacy.io/). It is more modern and has more methods nased baded on machine learning.
### ChatGPT's version of the Porter stemmer
ChatGPT produced working Python code that seems to implement the Porter stemmer.
- There is code for the five steps.
- The code is very readable.
- Some stemming does happen.
However, the results are not as expected. Some outputs are wrong and many are different than what NLTK produces.
You are encouraged to try that -- and with other algorithms too!
# Different kinds of words and how to deal with them
Some words are more useful for search than others.
## Content words and Function words
- **Content words**: *possess semantic content* and contribute to the meaning of the sentence in which they occur
	- nouns, lexical verbs, adjectives, adverbs
- **Function words**: which have very little substantive meaning and primarily *denote grammatical relationships* between content words
	- prepositions (in, out, under etc.), pronouns (I, you, he, who etc.) and conjunctions (and, but, till, as etc.).
## Content or function?
![[Pasted image 20240118132542.png]]
