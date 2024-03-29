## Windows Installations with MS SQL AD account

> On some versions of Windows 2012 you may need to install [Visual C++](https://www.microsoft.com/en-us/download/confirmation.aspx?id=14632)

### Using Windows AD account for SQL Authentication

* Copy ntlmauth.dll (from releases) to:
```
C:\Program Files\Papertrail\bin\sqlserver\x64 directory
```
* Copy sqljdbc_auth.dll (from Papertrail\bin\sqlserver\x64) to the below Java directories:
```
C:\Program Files\Java\jre1.8.0_181\bin
C:\Program Files\Java\jre1.8.0_181\lib
C:\Program Files\Java\jdk1.8.0_181\bin
C:\Program Files\Java\jdk1.8.0_181\lib
C:\Windows\System32
```

* Make sure the Windows account has access to the SQL DB.
* Change Windows Service > Log On > Log on as: {specify the domain account details} 
* Ensure that account has been granted "Logon as service" rights.
* Update papertrail.properties file by removing `db.user` and `db.pass` config, add:
 ```
 db.type=mssql
 db.url.config=;integratedSecurity=true
```

On a fresh installation of PaperTrail, you may need to manually seed the DB as the Configuration Wizard may not pass the AD credentials correctly in the JDBC string. To do this, run the below SQL scripts from the `Papertrail\deploy\scripts\sql\seed` directory in the correct order against the database.
```
01 mssql-create.sql
02 mssql-seed.sql
03 common-seed.sql
```

Then ensure that the papertrail.properties file has the ` db.url.config=;integratedSecurity=true` parameter set.
Also ensure that the below parameters are removed (to prevent entering the Configuration Wizard screen):
```
startup.roles=web,messaging,core
web.login.page=/web/webapps/wizard.html
```

Also important is to ensure that the domain account used for NTLM authentication is granted Full Control NTFS Permissions over the `Program Files\Papertrail` directory and the `Data` directory (Repository and Indexing)

## Windows Installations - character encoding issues
Windows encoding sometimes replaces characters (in outgoing emails, notes, etc) with odd characters, e.g. `aEU`<br>
This only affects PaperTrail instances running on Windows hosts. To resolve, add the below to the service.vmoptions / service_x64.vmoptions file and restart the PaperTrail service:<br>
`-Dfile.encoding=UTF-8`
