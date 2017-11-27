## Windows Installations with MS SQL AD account

> On some versions of Windows 2012 you may need to install [Visual C++](https://www.microsoft.com/en-us/download/confirmation.aspx?id=14632)

### Using Windows AD account for SQL Authentication

* Copy ntlmauth.dll to c:\Program Files\Papertrail\bin\sqlserver\x64 directory
* Make sure the Windows account has access to the SQL DB.
* Change Windows Service > Log On > Log on as: {specify the domain account details} 
* Ensure that account has been granted "Logon as service" rights.
* Update papertrail.properties file by removing 'db.user' and 'db.pass' config, add:
  db.type=mssql
  db.url.config=;integratedSecurity=true
