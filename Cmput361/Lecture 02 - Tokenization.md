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
