# Data Sources

Data sources allow for data to be looked up in a centralized fashion. These data sources are always referenced by name so they can differ in production and dev environments - both in parameters and type.

System properties can also be used for the URL, username and password
fields:
 

```javascript
${external.db.username} ${external.db.password} jdbc:mysql://${external.db.host}/`{.ini}
```

The properties can then be added to a .properties file in the Papertrail/conf installation folder

## JDBC

Connect to any remote database accessible via a JDBC URL examples of
which are:

`jdbc:mysql://host:3306/{db}`

`jdbc:sqlserver://host:1443;databaseName={db}`

`jdbc:postgresql://host:5432/{db}`

Parameters can be specified using **\${param}** syntax (they are
escaped to prevent SQL Injection):
 e.g.

`SELECT index1 as name, index2 as value FROM external_table WHERE index3 LIKE '${filter}'`

Note the **aliasing** to **name** and **value** is required to
correctly render in lookup fields/lists.

Although any parameter can be used, **\${filter}** is reserved for user
entered input.


## Local DB


A subtype of JDBC which connects to same database as PaperTrail and can be used
to query PaperTrail core tables, import and sync tables, or any other
table added to this db.
  

## Node Query

Returns the result of a PQL query - Commonly used for config nodes.
  

##Scripted

 Allows groovy script to be executed to return any arbritrary list of
data.
  

