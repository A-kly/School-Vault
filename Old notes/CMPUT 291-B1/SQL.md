- Structured Query Language  
	- standard query language for [[Relational Algebra|relational]] system  
	- developed in IBM Almaden (system R)  
- Some features  
	- Declarative: specify the properties that should hold in the result, not how to obtain the result  
	- Complex queries have procedural elements  
	- Set/Bag semantics  
- International Standards  
	- SQL1 (1986)  
	- SQL2 (SQL-92)  
	- SQL3 (SQL-99)  
	- Later extensions in 2003, 2006, 2008, 2011, 2016

Data definition component  
- CREATE TABLE table-name (col-defs, constraints)  
- DROP TABLE table-name  
- ALTER TABLE table-name action  
	- modifies the definition of a table where action is  
	- ADD (col-def)  
	- MODIFY (col-def)  
	- ADD constraint  
	- etc.  
- Data update component  
	- INSERT INTO table-name ...  
	- DELETE FROM table-name ...  
	- UPDATE table-name ...  
- Query Language

# Simple Queries
**Examples**:
Find the names of all branches with assets greater than $2,500,000
`branch (bname, address, city, assets)`
```sql
SELECT bname  
FROM branch  
WHERE assets > 2500000
```

_Simple predicates can be combined using AND, OR, NOT._
Find the names of all branches in Edmonton with assets greater than $2,500,000.
```sql
SELECT bname  
FROM branch  
WHERE assets > 2500000 AND city='Edmonton'
```

# Querying two Relations
**Examples**:
- List the name and the city of every customer who has an account with balance over $2,000.
`customer(cname, street, city)`
`deposit(accno, cname, bname, balance)`
```sql
SELECT customer.cname, city  
FROM customer, deposit  
WHERE balance > 2000  
AND customer.cname = deposit.cname
```
_This uses a [[Relational Algebra#Join (derived operator)|Join]] operator ( ⨝ ) between `customer` and  `deposit`_
![[Pasted image 20230126112001.png]]


- Find customers who have both loans and deposits.
`loan(accno, cname, bname, amount)`
`deposit(accno, cname, bname, balance)`
```sql
SELECT loan.cname  
FROM loan, deposit  
WHERE loan.cname = deposit.cname
```
- Equivalently using tuple variables.
```sql
SELECT l.cname  
FROM loan l, deposit d  
WHERE l.cname = d.cname
```
_Range variables (or tuple variables) are needed if the same relation appears twice in the `FROM` clause._

# A Simple Evaluation Algorithm

```sql
SELECT ...  
FROM R1 r1, R2 r2, ...  
WHERE C
```
- Tuple variables `r1, r2, ...` respectively range over rows of `R1, R2, ...`
- Evaluation strategy:
	- FROM clause produces Cartesian product of listed tables  
	- WHERE clause produces table containing only rows satisfying condition  
	- SELECT clause retains listed columns

```
for every tuple r1 in R1, r2 in R2, ...  
let r := r1 “concatenated” r2, ...  
if C(r) is true then  
output the desired columns
```
## From SQL to Relational Algebra

`loan(accno, cname, bname, amount)`
`deposit(accno, cname, bname, balance)`

```sql
SELECT l.cname  
FROM loan l, deposit d  
WHERE l.cname = d.cname
```

Equivalent to:  
![[Pasted image 20230126112939.png]]
# Queries With Set/Bag Results
- Find all cities of customers
```sql
SELECT city  
FROM customer
```
![[Pasted image 20230126113419.png]]
- To get rid of duplicates:
```sql
SELECT DISTINCT city  
FROM customer
```
![[Pasted image 20230126113432.png]]
- Duplicate rows not allowed in a relation . . . in _theory_  
- Duplicate elimination from query result is _costly and not automatically done_; it must be explicitly requested

# Working with Strings

Equality and comparison operators apply to strings (based on lexical ordering)  
- E.g. WHERE _cname_ < ‘P’

Concatenate operator applies to strings  
- E.g. SELECT _bname_ || ‘--’ || _address_

Expressions can also be used in SELECT clause  
- E.g. SELECT _bname_ || ‘--’ || _address_ AS NameAdd FROM branch

# Partial Matching

Find every customer whose street starts with “Avenue”.
`customer(cname, street, city)`
```sql
SELECT *  
FROM customer  
WHERE street LIKE ‘Avenue%’
```
- Expression: col-name `[NOT]` LIKE pattern
	- Pattern may include wildcard characters ‘%’ matching any string and '\_' (underscore) matching any single character.

# Naming the Results

For every deposit holder who has over $1000, find the customer name and the balance over $1000.
`deposit(accno, cname, bname, balance)`
```sql
SELECT cname, (balance - 1000) as bal  
FROM deposit  
WHERE balance > 1000
```

# Ordering the Results
Find the names and assets of all branches with assets greater than $2,500,000 and order the result in ascending order of asset values.
`branch (bname, address, city, assets)`
```sql
SELECT bname, assets  
FROM branch  
WHERE assets > 2500000  
ORDER BY assets
```
_Default is ascending order; a descending order can be specified by the DESC keyword._
_Not automatically sorted because its a costly operation._

# Queries Involving Set Operators

- set union:  
	- Q1 UNION Q2  
	- the set of tuples in Q1 or Q2  
- set difference:  
	- Q1 EXCEPT Q2  
	- the set of tuples in Q1 but not in Q2  
- set intersection:  
	- Q1 INTERSECT Q2  
	- the set of tuples in both Q1 and Q2

- Q1 and Q2 must be (almost) union-compatibles
	- same number/types of attributes, but the name of the attributes is irrelevant.

Eg:
List deposit holders who have no loans.
```
branch (bname, address, city, assets)  
customer(cname, street, city)  
deposit(accno, cname, bname, balance)  
loan(accno, cname, bname, amount)
```

```sql
SELECT cname  
FROM deposit  
EXCEPT  
SELECT cname  
FROM loan
```


List cities where there is either a customer or a branch.
```sql
(SELECT city  
FROM customer)  
UNION  
(SELECT city  
FROM branch)
```

Find all cities that have both customers and branches in.
```
branch (bname, address, city, assets)  
customer(cname, street, city)
```

```sql
(SELECT city  
FROM customer)  
INTERSECT  
(SELECT city  
FROM branch)
```

Find all cities that have a branch but no customer.

```
branch (bname, address, city, assets)  
customer(cname, street, city)  
deposit(accno, cname, bname, balance)
```

```sql
SELECT branch.bname, assets  
FROM branch, customer, deposit  
WHERE customer.city = ‘Jasper’  
AND customer.cname = deposit.cname  
AND deposit.bname = branch.bname
```
_What does this query do?_
>Finds the name and asset of every branch that has a deposit account holder  
>who lives in Jasper.

# Queries With Nested Structures

Queries within the WHERE clause of an outer query

```sql
SELECT  
FROM  
WHERE OPERATOR( SELECT ... FROM ... WHERE )
```
- There can be multiple levels of nesting
- Operators: `(NOT) IN, (NOT) EXISTS, < ALL, ...`
**Avoid nesting as much as possible!**

## Nested Structures Using “IN”

```sql
SELECT  
FROM  
WHERE expr IN (set of values  
				OR  
			another query)  
```
- E.g.  
	- ... WHERE province IN (‘AB’,‘BC’)  
	- ... WHERE province NOT IN (‘AB’,’BC’)

**Example**:
`deposit(accno, cname, bname, balance)`
```sql
SELECT cname  
FROM deposit  
WHERE bname IN  
	(SELECT bname  
	FROM deposit  
	WHERE cname = ‘Sunita’)
```
_Evaluate inner loop first_
- What does this query do?
	- _Finds every customer who has a deposit in some branch at which Sunita has a deposit._

**The Same Query Without Nesting**:
_Much better_
```sql
SELECT d1.cname  
FROM deposit d1, deposit d2  
WHERE d2.cname = ‘Sunita’ AND  
d1.bname = d2.bname
```

## Nested Structures Using “< ALL”,...

```sql
SELECT  
FROM  
WHERE expr < ALL (set of values)
```

- Other forms: `"<= ALL", "= ALL", ">= ALL",  "> ALL"` 
- Op ALL (set of values) evaluates to true <u>iff</u> the comparison evaluates to true for every value in the set.  
- Op SOME (set of values) evaluates to true <u>iff</u> the the comparison evaluates to true for at least one value in the set.

**Example**:
Find branches that have assets greater than the assets of all branches in Calgary.
`branch (bname, address, city, assets)`
```sql
SELECT bname  
FROM branch  
WHERE assets > ALL  
	(SELECT assets  
	FROM branch  
	WHERE city = ‘Calgary’)
```
_Select all assets from branches in Calgary, THEN select all branch names that are larger than ALL branch assets in Calgary_

## Nested Structures Using “EXISTS”

```sql
SELECT  
FROM  
WHERE (NOT) EXISTS( SELECT ... )
```
_Runs inner select clause and then, if that set is empty, `EXISTS` evaluates to false_
- `EXISTS (SELECT ...) `evaluates to true <u>iff</u> the result of the subquery contains at least one row.  
- The expression is evaluated for every iteration of the <u>outer query</u>.

**Example**:
Find the names of customers who live in a city with no bank branches.
`branch (bname, address, city, assets)  `
`customer(cname, street, city)`
```sql
SELECT cname  
FROM customer  
WHERE NOT EXISTS (SELECT *  
					FROM branch  
					WHERE customer.city=branch.city)
```
# Correlated vs Uncorrelated Queries
```sql
SELECT cname
FROM customer
WHERE NOT EXISTS(
	SELECT *
	FROM branch
	WHERE customer.city=branch.city)
```
**CORRELATED**
- Worse time complexity, inefficient
- like a nested for loop
- "costs" more
- uses _EXISTS_ keyword
	- Runs what's inside brackets once for _every_ item selected in outer section.
	- Recomputed for every row selected from customer

```sql
SELECT cname  
FROM customer  
WHERE city NOT IN(  
	SELECT city  
	FROM branch)
```
**UNCORRELATED**
- NOT like a nested for loop
- "costs" less
- uses _IN_ keyword
	- Subquery is computed once total and then outer section is run once

_Can be done with joins too_:
```sql
SELECT sname  
FROM Sailors S, Reserves R  
WHERE S.sid = R.sid
```
- More efficient solution and, in this particular case, simpler as well


# Division

- Query type: Find the subset of items in one set that are related to all items in another set 
- Example: Find customers who have deposit accounts in all branches.
![[Pasted image 20230131113004.png]]
_Strategy for implementing division in SQL_:
- Find set A, of all branches in which a particular customer c has a deposit account.
- Find set B of all branches.
- Output c if B–A is empty.
## SQL Solution 1

`branch (bname, address, city, assets)`
`deposit(accno, cname, bname, balance)`
```sql
SELECT c.cname  
FROM customer c  
WHERE NOT EXISTS  
(SELECT b.bname -- set B of all branches  
FROM branch b  
EXCEPT  -- set difference
SELECT d.bname  -- set A of branches in which  
				-- customer c has a deposit account  
FROM deposit d  
WHERE d.cname=c.cname -- CORRELATION!  
)
```
_Works out to `AllBranches - BranchesWherePersonHasDeposits`_

## SQL solution 2

Find customers who have deposit accounts in all branches.
- Same as “find all customers such that there is no branch where they do not have deposits in.”

```sql
SELECT c.cname  
FROM customer c  
WHERE NOT EXISTS  
	(SELECT bname  --branches where c has no deposits
	FROM branch b  
	WHERE NOT EXISTS  
		(SELECT *  --deposits of c into branch b
		FROM deposit  
		WHERE b.bname=deposit.bname  
		AND c.cname = deposit.cname))
```
_Notice how the scope of c and b are used in the inner nest. Their values are passed down from earlier in query_


# SQL and SQLite
- SQLite: pretty modern but light language
	- Released in 2000 (Oracle in 1977, DB2 in 1983)
	- It is light (intended for small devices)
	- Tightly integrated with applications (software library rather than a stand-alone system/process to communicate)
	- Locks the whole file/database during writes (not a good choice for write-intensive/concurrent transactions)
	- Supports both in-memory and on-disk databases
- Differences with SQL-92:
	- Does not support op ALL in nested queries
	- Does not support RIGHT OUTER JOIN and FULL OUTER JOIN
	- Views are read-only
	- ALTER TABLE command is very limited
	- Foreign keys constraints are not enforced by default
	- More left to be explored


# Basic Data Types in SQLite

- INTEGER
	- 1, 2, 3, 4, 6, 8 bytes integer (depending on the magnitude)
- REAL
	- 8 bytes floating point number
- TEXT
	- stored using database encoding (e.g. UTF-8)
- BLOB
	- stored as is
- NULL
	- null value
- NUMERIC
	- can store all other types; stored value is converted to INTEGER or REAL if the conversion is lossless and reversible

Others:
- INT, SMALLINT
	- INTEGER
- CHAR(n), VARCHAR(n)
	- TEXT
- DOUBLE, FLOAT
	- REAL
- DECIMAL
	- NUMERIC
- DATE, DATETIME
	- NUMERIC

# Joins
## Left Outer Join

```sql
SELECT E.eid, P.pid  
FROM Emp E, Proj P  
WHERE E.eid = P.eid
```
![[Pasted image 20230131114440.png]]
If we want to know an employee's info **even if they are not allocated to a project**, use this syntax:

```sql
SELECT E.eid, P.city  
FROM Emp LEFT OUTER JOIN Proj USING (eid);
```
_Goes from left to right. This means that we get all rows where `E.eid = P.eid`. The order there matters because when we get to e4, there is no `P.eid=e4` so we grab it anyways say its corresponding `pid=NULL`_

## Right Outer Join
Same but other way:
```sql
SELECT E.eid, P.city  
FROM Emp E RIGHT OUTER JOIN Proj P USING (city);
```

![[Pasted image 20230131115104.png]]
![[Pasted image 20230131115155.png|400]]
***Not supported in SQLite***

## Full Outer Join

```sql
SELECT *  
FROM Emp FULL OUTER JOIN Proj USING (city);
```

![[Pasted image 20230131115245.png]]
![[Pasted image 20230131115302.png|400]]
***Not supported in SQLite***


## Simulating FULL OUTER Join in SQLite

```sql
SELECT E.eid, P.pid, E.city  
FROM Emp E LEFT OUTER JOIN Proj P USING (city) 

UNION

SELECT E.eid, P.pid, P.city  
FROM Proj P LEFT OUTER JOIN Emp E USING (city)
```

## Alternative Syntax

```sql
SELECT *  
FROM from Emp LEFT OUTER JOIN Proj USING Emp.pid = Prj.pid
```

 1. join columns can have different names
 2. more general conditions are possible 
	 - (e.g. Emp.Salary < Mgr.Salary)
 3. two copies of ”same” column

# Aggregates

- Functions that operate on sets:
	- COUNT, SUM, AVG, MAX, MIN
- Produce numbers (not tables)
- Not part of relational algebra

Eg:
```sql
SELECT COUNT(*)  
FROM customer
```
```sql
SELECT MAX (assets)  
FROM branch
```

## Example 1
Find the number of customers in Edmonton.
```sql
SELECT COUNT(*)  
FROM customer  
WHERE city = "Edmonton"
```

## Example 2
Find the total assets of branches in Edmonton.
```sql
SELECT SUM(assets)  
FROM branch  
WHERE city = "Edmonton"
```

_See the DBMS’s SQL Reference for other aggregates_

## Use of Distinct in aggregates

Find the number of different branches where Xiaopeng has a deposit account.
```sql
SELECT COUNT(DISTINCT bname)  
FROM deposit  
WHERE cname = "Xiaopeng"
```
_Ignores repeating values in bname column_

## Aggregation & Nesting
Find the names of branches which have assets greater than the average assets of all branches.
```sql
SELECT bname  
FROM branch  
WHERE assets >  
	(SELECT AVG(assets)  
	FROM branch)
```
_This is an **uncorrelated** query_

>[!WARNING]
```sql
SELECT bname  
FROM branch  
WHERE assets >  
AVG(SELECT assets  
FROM branch)  
```
**This is not valid**

***
Find the number of customers who have deposit accounts in at least 3 different branches.
```sql
SELECT COUNT(*)  
FROM customer c  
WHERE 3 <=  
(SELECT COUNT(DISTINCT bname)  
FROM deposit d  
WHERE c.cname = d.cname
```
_Note that this is a **correlated** query_

# Grouping

*How to compute the number of customers per city?*

1. Have a separate query for each city:
```sql
SELECT COUNT(*)
FROM customer
WHERE city = "Edmonton"
```
- Cumbersome
- What if the number of cities changes?

2. define a special _grouping operator_:
```sql
SELECT city, COUNT(cname)
FROM customer
GROUP BY city
```
_Notice `GROUP BY`_

![[Pasted image 20230131120904.png]]
## Example

```sql
SELECT b.city, COUNT(b.bname), AVG(b.assets)  
FROM branch b  
GROUP BY b.city
```
![[Pasted image 20230131120952.png]]

## Syntax

```sql
SELECT a1, ..., ak, agg1, ..., aggl  
FROM R1, ...  
GROUP BY a1 ..., ak
```
*Every column name in the **SELECT** clause must appear in the **GROUP BY** clause (this is not required if the column name is only used in aggregation functions).*

_We can group by columns that were not selected in SELECT clause, but not vice versa_

>[!WARNING]
>This is illegal:
>```sql
>SELECT country  
>FROM Person  
>GROUP BY sex
>```
>_The attribute SELECT’ed is not unique per GROUP, "country" must have been in the GROUP BY clause_
>
>Also illegal:
>```sql
>SELECT country, avg(age)  
>FROM Person
>```

## Propper usage
For every student, list the id, the name and the average grade.

```sql
SELECT S.sid, S.name, AVG(grade)  
FROM Student S, Transcript T  
WHERE S.sid = T.sid  
GROUP BY S.sid, S.name -- this is correct, (GROUP BY S.sid) is not correct, SQLite does not enforce this!!
```

## HAVING Clause
- "*GROUP BY ...*" partitions tuples into groups where all tuples in a group have the same values.  
- "*HAVING ...*" is applied to each group separately to determine if the group as a whole qualifies.

_HAVING Filters the result of GROUP BY (like WHERE filters the result of select)_

### Example:
Find cities with more than two bank branches.
```sql
SELECT city  
FROM branch  
GROUP BY city  
HAVING COUNT(*) > 2
```

## Evaluation of GROUP BY with HAVING
![[Pasted image 20230131121531.png]]

### Example:

For every branch, list the branch name and the name of every customer who has more than 3 loans each over $100,000 in that branch.

```sql
SELECT bname,cname -- we can add (COUNT(accno)) if we wanted to know how many accounts one has
FROM loan  
WHERE amount > 100000  
GROUP BY bname, cname  
HAVING COUNT(*) > 3
```

***MORE EXAMPLES ONLINE***
### Example:
![[Pasted image 20230202112740.png]]

## Aggregates: Proper Usage

`SELECT d.cname, AVG (d.balance)`
- **makes no sense (in the absence of GROUP BY clause)**

`SELECT COUNT (*), AVG (d.balance)`
- *this is OK*

`WHERE d.balance > AVG (SELECT ....)`
- **aggregate cannot be applied to SELECT statement**
# More Commands

## Updates - Insert
![[Pasted image 20230202113406.png|500]]
## Updates - Bulk Insert
![[Pasted image 20230202113425.png|400]]
## Updates - Delete and Update
![[Pasted image 20230202113509.png|300]]

## Examples
![[Pasted image 20230202114214.png]]
![[Pasted image 20230202114233.png]]

## View
**The point**: _Show only some data to a user, provide them an easy way to access the data_
![[Pasted image 20230202114321.png]]

## Examples

Create a view (called cust_info) which has for each customer the name, city, the number of deposit accounts they own and the total balance.
```sql
CREATE VIEW cust_info(Name, city, Num, Total)
AS SELECT c.cname, city, COUNT(accno), SUM(balance)
FROM deposit d, customer c
WHERE d.cname=c.cname
GROUP BY c.cname, city
```


Create a view (called deposit_holders) which includes the name and the city of every deposit account holder.
```sql
CREATE VIEW deposit_holders(Name, city)  
AS SELECT distinct c.cname, city  
FROM deposit d, customer c  
WHERE d.cname=c.cname
```

## Views: A Summary

- View = query ≅ table 
- A derived table whose definition, not the table itself, is stored. 
- Provides a degree of data independence.  
- Queried like a table.  
- Updated under some conditions

## View Updates

![[Pasted image 20230202114629.png]]
![[Pasted image 20230202115928.png]]

# NULL

Unknown Value

- Useful when we don’t know a column value
	- very common in practice.
- Simple usage in queries:
	- ... WHERE phone IS NULL
	- ... WHERE phone IS NOT NULL
	- SELECT cname FROM CUSTOMER WHERE city IS NOT NULL

- SELECT cname FROM CUSTOMER WHERE city = "Edmonton"
	- What happens if city for some customers is NULL?
	- _Customers with NULL are not selected_
	- 

- The predicate city="Edmonton" evaluates to UNKNOWN when city is NULL.  
	- the customer name will not be output  
- What if the WHERE clause consists of several predicates?  
	- E.g. city="Edmonton" OR street LIKE "100%"  
	- use three-valued logic: values TRUE, FALSE, UNKNOWN.  
- NULL is not a constant!

## Set Operations
![[Pasted image 20230202120308.png]]

# Constraints in SQL/92

Already seen: primary key and foreign key constraints.  
- NOT NULL  
	- specifies that an attribute cannot contain null values  
	- should be specified for all primary keys (if it is not default)  
- UNIQUE  
	- specifies the alternate keys  
- Domain Constraints  
- CHECK Constraints

## Example:

```sql
CREATE TABLE branch(  
bname CHAR(15) UNIQUE,  
address VARCHAR(20),  
city CHAR(9) NOT NULL,  
assets DECIMAL(10,2) DEFAULT 0.00  
)
```

## User-Defined Domains
```sql
CREATE DOMAIN Gender AS CHAR(1)
```
_Add some domain constraints  _
```sql
CREATE DOMAIN Gender AS CHAR(1)  
CHECK (VALUE = "M" OR VALUE = "F" OR VALUE = "X")
```
```sql
CREATE DOMAIN Gender AS CHAR(1)  
CHECK (VALUE IN ("M","F","X")) 
```
```sql
CREATE TABLE TEMP ( ..., sex Gender, ...)
```

## Domain Constraints
_Specifies the condition that each row has to satisfy, Violations are rejected._
```sql
CREATE TABLE branch  
(bname CHAR(15)NOT NULL,  
address VARCHAR(20),  
city CHAR(9),  
assets DECIMAL(10,2) DEFAULT 0.00  
CHECK (assets >= 0));
```

# Assertions
Global constraints of the form  
`CREATE ASSERTION name CHECK (condition)`
Example: No branch can have a customer who has more than 2 loans over  
$100,000.

```sql
CREATE ASSERTION deposit CHECK  
(NOT EXISTS  
(SELECT bname, cname  
FROM loan  
WHERE amount > 100000  
GROUP BY bname, cname  
HAVING COUNT(*) > 2));
```
_Assertions are not also supported in SQLite. It does support triggers (seen in CMPUT 391,  
http://www.sqlitetutorial.net/sqlite-trigger/)_

# Summary

- Covered different types of queries
	- Simple, multi-table, nested (correlated and uncorrelated) aggregate, grouping
	- Update commands, constraints, NULL, VIEWs
	- There are other things we did not cover, e.g., “triggers”
- Be aware of syntactic differences between different flavors SQL and, also limitations of the DBMS itself
	- RTFM’ing is unavoidable
		- "Read the Fucking Manual"
		- 

# Other Features and Commands
**Use SQL statements inside a host language**

Advantages:
- Can do all the fancy things you do in C/Java/Python.
- Still have the power of SQL.

Need mechanisms for
- Embedding SQL statements in code
- Transferring data to/from DBMS
- Compiling and linking the program.

# SQL inside Applications

- _[[#Statement-level interface]]_
	- SQL statements appear as new statements in the program. 
	- Precompile step: replaces new statements with some procedure calls. 
	- Flavors: Static SQL, Dynamic SQL  
- _Call-level interface_
	- Program is written entirely in the host language
	- No precompile step.
	- SQL statements are passed as parameters to some procedures.
	- Flavors: ODBC, JDBC, sqlite callback

## Statement-level Interface
`EXEC SQL <sql statement>`
![[Pasted image 20230207111415.png]]
- Static
	- `cnt` is local var in program and plugged into statement and `cnt` is _usable in the rest of the program_
- Dynamic
	- generating sql queries on the fly,
### Program Structure
![[Pasted image 20230207111440.png|400]]
_Commit is everything is good, rollback if something goes wrong_
## Include statements

- An essential one: SQL Communication Area
- `#include <sqlca.h>` , OR
- EXEC SQL INCLUDE SQLCA
- It provides runtime status information including:
	- `sqlca.sqlcode`: the return code of SQL statements
	- `sqlca.sqlerrm`: the error messages (if any) 
		- `sqlca.sqlerrm.sqlerrmc` : error message
		- `sqlca.sqlerrm.sqlerrml` : the length of the error message

## Host Variables

- Used to pass values between a SQL statement and the rest of the program.
- Declaration: as follows:
```c
EXEC SQL BEGIN DECLARE SECTION;  
/* all host variable declarations go here */  
int cnt;  
char name[20];  
EXEC SQL END DECLARE SECTION;
```
- Usage in SQL statements:  `EXEC SQL SELECT COUNT(*) INTO :cnt FROM emp;`
	- The variable must be preceded with ':' to distinguish it from SQL identifiers.

## Error Handling
- Check `sqlca.sqlcode`, the return code of SQL statements 
	- == 0 : the command was successful 
	- 0 : no row in the output  
	- < 0 : error
- Use WHENEVER statements: e.g.  
```c
EXEC SQL WHENEVER SQLERROR GOTO lbl1;  
EXEC SQL WHENEVER NOT FOUND GOTO lbl3;  
EXEC SQL WHENEVER SQLERROR DO err_func();  
EXEC SQL WHENEVER SQLERROR CONTINUE;
```
Example:
```c
EXEC SQL DROP TABLE emp;  
if (sqlca.sqlcode == 0) {  
printf(“Table emp is successfully dropped\n”);  
}  
else {  
sqlca.sqlerrm.sqlerrmc[sqlca.sqlerrm.sqlerrml] = ‘\n’;  
printf(“Oracle error: %s\n”, sqlca. sqlerrm.sqlerrmc);  
}
```

# myprog.pc: Our first program

```c
#include <stdio.h>  
EXEC SQL INCLUDE SQLCA;  
int main(int argc, char *argv[]) {

	EXEC SQL BEGIN DECLARE SECTION;
		char user[10] = “SCOTT”;
		char pwd[10] = “TIGER”;
	EXEC SQL END DECLARE SECTION
	
	EXEC SQL WHENEVER SQLERROR GOTO error;
	EXEC SQL CONNECT :user IDENTIFIED BY :pwd;
	printf(“connected to Oracle”)
	
	/* SQL statements */
	EXEC SQL COMMIT RELEASE;
	return 0;
	error:
		sqlca.sqlerrm.sqlerrmc[sqlca.sqlerrm.sqlerrml] = ‘\0’;
		printf(“Oracle Error: %s\n”, sqlca.sqlerrm.sqlerrmc);
		EXEC SQL WHENEVER SQLERROR
	CONTINUE;
		EXEC SQL ROLLBACK RELEASE;
		return 1;
}
```
![[Pasted image 20230207113026.png|400]]

# myprog2.pc: Our 2nd Program

```c
* get the emp_number from input and print the emp_name */  
...  
EXEC SQL BEGIN DECLARE SECTION;  
	int emp_number;  
	char emp_name[30];  
EXEC SQL END DECLARE SECTION;  
EXEC SQL WHENEVER SQLERROR GOTO error;  
EXEC SQL WHENEVER NOT FOUND GOTO nope;  
/* Connect to the database ... (refer to our “1st program”) */  
printf(“Enter emp_number:”);  
scanf(“%d”, emp_number);  
EXEC SQL SELECT ename INTO :emp_name  
	FROM emp  
	WHERE empno = :emp_number;  
printf(“Employee name is %s\n”, emp_name);  
return 0;  
error: ...  
nope: ...
```

# Complications

- What if a host variable is assigned a NULL?
	- not a constant.
	- solution: use an extra indicator variable.  
- What if a SQL statement returns more than one row?
	- cannot fit it in any C variable!
	- solution: use a cursor.

## Indicator Variables
![[Pasted image 20230207113354.png|500]]
_`emp_name_ind` is an indicator variable to check if value is NULL, (indicator variable is -1)_
## Use of a Cursor
![[Pasted image 20230207113448.png|400]]
_get output with multiple rows, lets the outer program navigate through rows to get all values of selected rows_
- Result set – set of rows produced by a SELECT statement
- Cursor – pointer to a row in the result set.
- Cursor operations:∙
	- Declaration∙ 
	- Open – execute SELECT to determine result set and initialize pointer∙ 
	- Fetch – advance pointer and retrieve next row∙ 
	- Close – deallocate cursor
![[Pasted image 20230207115057.png]]

## Summary
![[Pasted image 20230207115134.png]]

# Call-level Interface
- Neither the schema nor the database needs to be known at compile time.
- The application can connect to more than one database.
![[Pasted image 20230207115207.png]]
_Documents stored in a relational database is not really feasible_
_Often (eg. instagram) one relational database and one other database to store the data_
## Executing a Query (using Java now)
![[Pasted image 20230207115336.png|500]]
![[Pasted image 20230207115412.png]]
## Result Sets and Cursors

- _Three types_ of result sets in JDBC:
	- _Forward-only_: not scrollable
	- _Scroll-insensitive_: scrollable (can jump up and down in the result set!), changes made to underlying tables after the creation of the result set are not visible through that result set
		- eg. static snapshot
	- _Scroll-sensitive_: scrollable, changes made to the tuples in a result set after the creation of that set are visible through the result set
		- eg. stock market

### Result Set
![[Pasted image 20230207115832.png]]
## SQLite callback in C

Three functions: open, exec, close
- `sqlite3_open(const char *filename, sqlite3 **db)`
- `sqlite3_exec(sqlite3 *db, const char *sql,`
- `sqlite_callback, void *data, char **errmsg)`
- `sqlite3_close(sqlite3 *db)`
Output is processed by a callback function

## More Information

- Statement-level Interface:
	- Not supported in SQLite
	- But is supported in other databases such as Oracle
- Call-level Interface
	- JDBC tutorials
	- Callback interface in C

- **Final note (but quite important):**
	- **Avoid data processing in the host language if it can be passed on to the DBMS / SQL.**
	- Use the host language **ONLY** for things that cannot be done in SQL.