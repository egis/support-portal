## Data Sources

A DataSource is a generic abstraction over access and querying databases, it can be linked directly to List, and called via the front-end using `/data/{datasource name}/`. 

The type of datasource can also be switched (provided the name is retained) to allow different implementations during production / staging etc..

-   Database connections are pooled based on connection string and username.
-   Column headers and index values must match index values in
    PaperTrail, otherwise give columns aliases by using the “AS” function.
-   All native SQL commands and functions can be used in the statement.
-   Separate columns in SELECT statements by commas.
-   If column names contain spaces, double quotes (“ “) should be used
    to surround the name in order to concatenate the name.

 
> It is recommended to use system properties to specify the URL, Username and Password so that they can be externalized and reused across multiple rules. e.g. `${lob.db.url}`


Paramaters are passed via `${param1}` expressions e.g.

```sql
 SELECT * FROM Invoices WHERE Invoice_No = '${invoice_no}
```

Using `UPDATE`, `DELETE`, `EXEC` or `INSERT` SQL keywords will use [PreparedStatement.executeUpdate()](https://docs.oracle.com/javase/7/docs/api/java/sql/PreparedStatement.html#executeUpdate()) while all other Keywords will use [PreparedStatement.executeQuery](https://docs.oracle.com/javase/7/docs/api/java/sql/PreparedStatement.html#executeQuery())

## Direct Access

You can also use direct JDBC or the SQLUtils library to access external databases via a runScript rule - Ensure that you follow the pattern below

```groovy
import com.egis.datasource.JdbcDataSourceCache
import com.egis.kernel.Kernel
import com.egis.utils.SQLUtils
import javax.sql.DataSource

String url = System.getProperty("lob.db.url");
String username = System.getProperty("lob.db.username");
String password  = System.getProperty("lob.db.password");
DataSource ds = Kernel.get(JdbcDataSourceCache.class).get(url, username, password)

SQLUtils.executeStatement(ds, "EXEC sp.StoreProc(?,?,?)", "param1", "param2", "param3")
```

> Note that a `Connection` or `DataSource` is not created directly but delegated to `JdbcDataSourceCache` so that connection pooling can occur

# Database JDBC Configs

| Server | Configuration 
| ---------- | ---------
| Microsoft SQL Server | `jdbc:sqlserver://[serverName[\instanceName][:portNumber]];databaseName=<databaseName>[;property=value[;property=value]] ` or `jdbc:sqlserver://host;databaseName=test123`
| MYSQL | `jdbc:mysql://<database server>:<ports>/<database names>`
| PostgreSQL | `jdbc:postgresql://<database server>:<port>/<databaseName>`

## SQL
  
SELECT Statement : To Fetch records from an external database to PaperTrail records.  

Format : 
```javascript
   **SELECT \<COLUMNS\> FROM \<TABLENAME\> WHERE
   \<DATABASE INDEX\> = \${\<PAPERTRAIL INDEX\>}**
```

```javascript
   SELECT No_ AS Invoice_No, 
     LEFT(CONVERT(date, "Posting Date"),10) 
     AS Invoice_Date,"Order No_" 
     AS Internal_Order, "Sell-to Customer No_" 
     AS Customer_No,"External Document No_" 
     AS Customer_Order_No, "Shipment Method Code" 
     AS Delivery_Method 
   FROM "SAFINTRA JHB$Sales Invoice Header" 
   WHERE No_ = '${invoice_no}
```

UPDATE Statement : To Update records from an external database to PaperTrail records.  

Format :
```javascript
**FORMAT**: **UPDATE \<TABLE NAME\> SET \<DATABASE INDEX\> =
'\<VALUE\>' WHERE \<DATABASE INDEX\> = \${\<PAPERTRAIL
INDEX\>}**
```

```javascript
UPDATE test 
SET Index1 = 'asdf' 
WHERE Invoice_Number = ${Invoice_Number}
```

## Rules for SQL statements

-   Column headers and index values must match index values in
    PaperTrail, otherwise give columns aliases by using the “AS”
    function.
-   All native SQL commands and functions can be used in the statement.
-   Separate columns in SELECT statements by commas.
-   If column names contain spaces, double quotes (“ “) should be used
    to surround the name in order to concatenate the name.

 

## Event 

When to run the SQL Lookup or Update.

