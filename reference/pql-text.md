# PQL


PQL is an SQL-like language that can be used for querying and filtering data in PaperTrail. It can be used in the following places:  

* Anywhere where a query expression is used e.g. Advanced Search Reports, Queues, Scheduled Rules, Document linking etc.

* As an alternative to groovy based expressions on node rule filters
  e.g. instead of:
  `filename == 'filename && a == 'b'`
  Use:
```sql
WHERE filename = 'filename' AND a = 'b'
```

PQL filters are fully case-insensitive and null safe so instead of: 

`index1 != null && index1.toLowerCase() == 'abc'`  
Use:
`WHERE index1 = 'abc'`

## Syntax

The `SELECT` clause MUST contain exactly one of the following:

* A comma-separated list of one or more column names (node or document index names).  
    - You can use aliases to rename returned columns, e.g. column AS alias.  
    - If an explicit column list is provided: Only the columns listed will be returned and only in the order supplied.  
    - Note : All standard indexes and any custom indexes will be returned in the default order  
    - Note : Only custom indexes will be returned 


* One or more calls to aggregate functions.
    - Aggregate functions produce a single row output from multiple rows in a group.


## Column Expressions

Groovy expressions can be used to format data returned e.g. 

```sql
SELECT '${name[0]}' as Initial FROM Clients
```

Multiple columns can also be referenced:
```sql
SELECT '${LastName}, ${FirstName}' as FullName FROM Clients
```

As well as arithmetic on Number and Double indexes:
```sql
SELECT '${total + vat}' as GrandTotal FROM 'Sales'
```

## Wildcards
Plain SQL wildcard works as expected - e.g. `SELECT * FROM 'Sun/Clients'` selects all the standard and custom indexes 
from Sun/Clients node. There's also doublewildcard syntax:
```sql
SELECT ** FROM 'Sun/Clients'
```
- this selects only custom indexes. 

## FROM Clause

The FROM clause identifies which Virtual Table (Node) the query will be run against, as described in the previous section.

The FROM clause MUST contain the full path of a node, and MUST be single quoted if there are any spaces .e.g

`FROM parent/division`
`FROM 'parent/sub folder/folder'`

## WHERE

This clause identifies the constraints that rows MUST satisfy to be considered a result for the query.

All column names MUST be valid “queryName” or their aliased values for properties that are defined as “queryable” in the Object-Type(s) whose Virtual Tables are listed in the FROM clause.

Properties are defined to not support a “null” value, therefore the <null predicate> MUST be interpreted as testing the not set or set state of the specified property.

 Comparisons permitted in the WHERE clause.

PQL supports the following predicates:

* = (equals)  
* \> (bigger than, after)  
* < (smaller than, before)  

> Note: Bigger than / Less than and end equal to (>=, <=) are not supported

Date values can be relative e.g.:

```sql
SELECT docId FROM queryTests2 WHERE date1 > '+7d'
```
* contains
* not contains
* startsWith
* not startsWith
* endWith
* not endsWith
  BETWEEN and NOT BETWEEN predicates to compare on ranges
  e.g. column BETWEEN a AND b, is equivalent to column >= a AND column <= b 

* IN  
* LIKE   
* IS NULL  
* IS NOT NULL  
* all_empty  
> e.g. a filter that matches when all 4 indexes are populated
> WHERE not all_empty (invoice_no,total,date,approved)
* not all_empty  
* before, after   

```sql
WHERE createdDate BEFORE '2015-01-01'
```

### WHERE Expressions

Expressions can also be on both the left and and right side of WHERE clauses. e.g.

```sql
SELECT name FROM Customers WHERE '${name[0]}' = 'A'
```
OR
```sql
SELECT number1 FROM queryTests2 WHERE 99 > ${number1 + pqldouble1}
```

## ORDER BY

* This clause MUST use a single column to order by.
* All column names referenced in this clause MUST be valid “queryName” or alias (either for an aggregate function result or a column).
* Only columns in the SELECT clause MAY be in the ORDER BY clause.
* `ORDER BY docId DESC` doesn't currently work - use `ORDER BY createdDate DESC` instead 

## LIMIT N
LIMIT N construct is supported - e.g. 
```sql
SELECT * FROM 'MyBank/KYC' WHERE loan_id=5 ORDER BY createdDate DESC LIMIT 1
```
will select last doc from `MyBank/KYC` node with given filter.

## GROUP BY

This clause specifies one or many columns to group by.

Supported functions:

* `COUNT(column`, `COUNT(*)` - returns a number of entries in a group. `COUNT(column)` skips null values.
* `AVG(column)` - returns an average value of a column in a group.
* `MIN(column)`, `MAX(column)` - return a minimal or maximal value of a certain column in a group.
* `SUM(column)` - returns a sum of a column in a group.

Column references can also include groovy expressions e.g. 

```sql
SELECT sum(${time/60}) FROM Time  GROUP BY createdBy
```

## HAVING
Having is used to filter on values that have been grouped e.g.

```sql
SELECT text1, SUM(number1) FROM queryTests2 GROUP BY text1 HAVING SUM(number1) > 10
```
OR
```sql
SELECT text1, SUM(\${number1 * 10}) AS totals FROM queryTests2 GROUP BY text1 HAVING totals > 1000
```

## Escaping

Repositories MUST support the escaping of characters using a backslash `\` in the query statement.  The backslash character `\` will be used to escape characters within quoted strings in the query as follows:

* \’ will represent a single-quote(‘) character
* \ \ will represent a backslash `\` character
* Within a LIKE string, `\%` and `\_` will represent the literal characters % and _, respectively.
* All other instances of a \ are errors.


## Virtual Data Sources

`FROM '@{VirtualDataSource}`


##  @WorkflowHistory


The workflow history virtual data source will return details about the unassigned and human tasks of a one or more documents e.g. 

```sql
SELECT * FROM '@WorkflowHistory' WHERE docId = 1
```
Will return the following special columns:

| Column                 | Description                              |
| ---------------------- | ---------------------------------------- |
| position               | The workflow label of the task           |
| start                  | The start date of the task               |
| end                    | The end date of the task                 |
| workflow               |                                          |
| allocation             | The final user allocated                 |
| createdBy              | Who the allocation was created by. This is not the creator of the document. |
| duration               | The duration of the task e.g. 12 hours   |
| durationMillis         |                                          |
| businessDuration       | The duration of the task while in business hours e.g. 2 hours |
| businessDurationMillis |                                          |

Any standard and custom indexes can also be merged into the results by adding them into the column list.
Any standard search criteria can also be used

##  @Activity

Returns: 

* Document creations 
* New Notes 
* Audits of configurable type = defaulting to Check In, Forward, Delete 

```sql
SELECT * FROM @Activity WHERE Node = 'Finance' AND user = 'X' 
```
equivalent to: 
```sql
SELECT * FROM @Activity/Finance WHERE user = 'X' 
```
`date` is used for searching on the activity date (not the date of the document)
```sql
SELECT * FROM @Activity WHERE date = '-7d' 
```

| Column   | Example                           |
| -------- | --------------------------------- |
| user     | The user who performed the action |
| date     | The date the action was performed |
| filename |                                   |
| node     | The full node path                |
| docId    |                                   |
| audit    | e.g. Allocated                    |
| type     | e.g. to: John Doe                 |



##  @Queue

```sql
SELECT * FROM @Queue/{queueName}
```

| Column      | Example |
| ----------- | ------- |
| queue       |         |
| user        |         |
| sla         |         |
| time_avg    |         |
| time_median |         |
| time_95     |         |
| processed   |         |
| skipped     |         |
| taken       |         |
| currentSize |         |

## @LDAP

```sql
SELECT sAMAccountName,name,email FROM @LDAP
```



## @ds

Queries [data sources](../integration/data-sources-text.md)

```sql
SELECT * FROM @ds/{data source name} WHERE param = '123'
```
