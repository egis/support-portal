# Backups

What needs to be backed up?
---------------------------

-   Database and transaction logs
-   File Repository (Everything under PT\_Repo)
-   SSL Certificate : conf/keystore (If configured)
-   Encryption Keys : e.g. conf/keys.\* If File store encryption is
    configured
-   Indexes : Only for very large installations where an index rebuild
    is too time-consuming


How to backup?
--------------

To backup in PostgreSQL 

```java
cd "C:\Program Files"
cd PostgreSQL\9.2\bin
pg_dump –U postgres –h localhost {postgresdb} > ”C:\{location}\{location}{backupname}.sql”
psql -U postgres -h localhost {pt8} > C:\{location}\{location}{backupname}.restore.sql
```

To backup in MySQL 

```java
cd MySQL\MySQL Server 5.1\bin
C:\ProgramFiles\MySQL\MySQL Server 5.1\bin>mysql -u {username} -p {password} {MYSQL db} < "e:\database.sql"
```

Backups in MSSQL can be done from the management console.

Schedule Database Backups using PaperTrail
------------------------------------------


 Papertrail can automatically backup databases on schedule configured
under Services  → Properties  → Backup → DB Schedule
(db.backup.schedule).

 PaperTrail will run the pgdump, mysql\_dump or SQL Server Backup
Database command  and store the result in the file repository. 

Note: Backups can only be made of local database

 Configuring cloud backups
--------------------------

Cloud backups lets you back up the PaperTrail file repository (and optionally the PaperTrail database) in near real time to the [Amazon S3 cloud](http://aws.amazon.com/s3/).

 If you set up the Amazon S3 account, use the information from that
account to configure cloud backups. For Egis managed backups, Egis will
supply the information to you.

 1. From Services  →  Tasks →  Wizards, select Configure cloud backups.
Enter the values of the Amazon S3 account in these fields:\
 2. **Bucket** The Amazon S3 bucket to use, for example:
acme.papertrail\
 3. **Access key** An access key that has read and write permissions to
the bucket.\
 4. **Secret key**

Configuring periodic Windows file share backups
-----------------------------------------------

PaperTrail creates an incremental backup ZIP file and copies the ZIP
file to the specified shared folder.  

Specify these options under the Backup Settings page of the
installation wizard or after installation via Services →  Tasks → 
Wizards  → 

Configure Windows Share backups
-------------------------------

1. Host – the hostname of the Windows or SMB/CIFS based fileserver\
1. Backup Dir – The share and path location (e.g.,
Backups/Papertrail Relative to the file share, not relative the root
director)
1. Username and Password if applicable

Ad-Hoc Backup
-------------

Typically, do an ad-hoc backup before you upgrade PaperTrail or before
you migrate to a different server.  
 An ad-hoc backup will export all the files in the repository to a local
or windows file share location. Multiple ZIP files will be created; a
log file for each ZIP file will also be created containing the names of
the files in the corresponding ZIP file.  

 An ad-hoc backup can be re-run using the same destination path, the
logs files will be read and only new files added will be backed up.  
1. Under Services → Tasks → Backups → Backup Repository  
2. Destination: Local or windows file share
(`smb://user@pass:host/Share/folder`)  
3. Optional: Check verify to verify the backup once complete  
4. Max File Size: Enter a maximum file size. Once a backup file
reaches this limit (it may not be exact depending on the size of
individual files) a new backup file will start.

Restoring from backup
---------------------

Select Restore from Windows File Share or Cloud from the installation
wizard.

3rd Party backup
----------------

1. Backup the database and applicable transaction logs.
2. Backup the PT\_Repo directory (defaults to C:\\Data\\PT\_Repo).

> Note: PaperTrail does not update files in the PT\_Repo directory so once
backed up a file does not need to backed-up again.

3.    For large installations the indexes can also be backed up to
decrease restore times  
 Under Services  → Properties  → Backup  Specify an Index Backup
Schedule & Directory

Native restore from backup
--------------------------

1. Restore database and file repository to original locations
2. Install PaperTrail
3. Check new installation and enter existing database details

## Migrate PaperTrail to another host
1. On the current server, perform a dump of the DB. Refer to [how to backup](backups-text.md/#how-to-backup)
2. On the new server, install the pre-requisites (Java 8 SDK, LibreOffice, DB application) and create the DB. DO NOT install PaperTrail as yet
3. Import the DB dump onto the new server. Example Postgres command:
 * `psql -U postgres papertrail < C:\PTBackup\20170302.sql`
4. Run the SQL command to update the license on the new server:
 * `update system_property set value = '[License Text]' where name ='license'`
5. Copy over the PT_Repo and PT_Index directories to the new server
6. Complete the [install of PaperTrail](../installation/server-installation.md) on the new server
7. Copy the following files from the OLD PaperTrail server to the NEW PaperTrail server:
 * services_x64.vmoptions
 * any customer .jar files in the deploy directory
 * MySQL ONLY - copy mysql-connector-{version} from libs directory
