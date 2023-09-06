one of many types of [[Databases]]

# Document Collections
- *Collection:* is a group of MongoDB documents. It is the equivalent of an RDBMS table. A collection exists within a single database.  
- *Document:* records are documents which behave a lot like JSON files. JSON data is written as name/value pairs. A name/value pair consists of a field name (in double quotes), followed by a colon, followed by a value. So each document is a set of key-value pairs.

# MongoDB Concepts
- MongoDB is a cross-platform, document database which belongs to a family of databases called NoSQL - **Not only SQL**.  
- MongoDB works on concept of collections and documents.  
- *Database:* a physical container for collections. A single MongoDB server typically has multiple databases.
- **Collections do not enforce a schema**.
- Documents have dynamic schema. Dynamic schema means that documents in the same collection do not need to have the same set of fields or structure, and common fields in a collection's documents may hold different types of data.
- Having said that, typically all documents in a collection are of similar or related purpose.
![[Pasted image 20230323111414.png]]
## Sample MongoDB Document

```json
{
	_id: ObjectId(7df78ad8902c)
	title : ' MongoDB Overview '
	description : ' MongoDB is no sql database '
	by : ' tutorials point '
	url : ' http: / / www. tutorialspoint . com' ,
	tags : [ 'mongodb ' , ' database ' , 'NoSQL' ] ,
	likes : 100,
	comments : [
		{
			user : ' userl '
			message : 'My first comment' ,
			dateCreated: new Date(2011, 1, 20, 2, 15),
			like: O
		},
		{
			user : ' user 2 '
			message : 'My second comments '
			dateCreated: new Date (2011, 1, 25, 7, 45),
			like : 5
		}
	]
}
```
- \_id: is a 12 bytes hexadecimal number which assures the uniqueness of every document. You can provide \_id while inserting the document. If you don’t provide it then MongoDB provides a unique id for every document.  
- MongoDB provides two types of data models: Embedded data model and Normalized data model. Based on the requirement, you can use either of the models while preparing your document.  
- *Embedded Data Model:* In this model, you can have (embed) all the related data in a single document, it is also known as de-normalized data model.
## Embedded Document
![[Pasted image 20230323112146.png]]
Again, *In this model, you can have (embed) all the related data in a single document, it is also known as de-normalized data model.*
## Normalized Documents
![[Pasted image 20230323112423.png]]
*Separate documents for each entity. We relate them together with the ID of their associated entity*
## How to setup
![[Pasted image 20230323112554.png]]
## MongoDB server
![[Pasted image 20230323112607.png]]
## MongoDB Client
![[Pasted image 20230323112708.png]]
## Database Commands
![[Pasted image 20230323112732.png]]

**You have to R.T.F.M.**
https://docs.mongodb.com/manual/

## Collection Commands
![[Pasted image 20230323112835.png]]
![[Pasted image 20230323112900.png]]
## Commands
![[Pasted image 20230323112915.png]]
![[Pasted image 20230323112931.png]]
![[Pasted image 20230323112949.png]]
![[Pasted image 20230323113240.png]]
![[Pasted image 20230323113314.png]]
## Helpful commands
![[Pasted image 20230323113352.png]]
![[Pasted image 20230323113407.png]]
# Create index
![[Pasted image 20230323113640.png]]
![[Pasted image 20230323113653.png]]
# Projection
![[Pasted image 20230323113816.png]]
# Aggregations
![[Pasted image 20230323113836.png]]
## Example
![[Pasted image 20230323115234.png]]
*Output is 860 ONLY IF COLLECTION ENDS AT BOTTOM*
![[Pasted image 20230323115304.png]]
![[Pasted image 20230323115313.png]]
![[Pasted image 20230323115333.png]]
![[Pasted image 20230323115535.png]]
*Sum is greater than140 because of  the '...'*
## SUM, COUNT, etc.
![[Pasted image 20230323115625.png]]

## Unwinding
TURNS
![[Pasted image 20230323115734.png]]
INTO
![[Pasted image 20230323115745.png]]
*Unwinding take embedded documents and separates them into individual entities*
# JOIN
![[Pasted image 20230323115926.png]]
# Aggregation (JOIN)
![[Pasted image 20230323115947.png]]

# Pipelining
- In Relational Algebra we had the “relation-in-relation-out” model  
- In MongoDB we use pipelines to process documents in stages using a “document-in-document-out” model
![[Pasted image 20230323120022.png]]
# Shutdown process
![[Pasted image 20230323120039.png]]
# Sidenote: Using MongoDB on lab machines
![[Pasted image 20230323120102.png]]
# Cleaning things up
![[Pasted image 20230323120136.png]]
# MongoDB + Python?
![[Pasted image 20230323120154.png]]
