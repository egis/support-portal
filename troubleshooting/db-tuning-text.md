# Database Performance Tuning

-   Use READ COMMITTED default tx isolation level.
-   Use a transaction logging mode that allows point in time recovery
    (PITR) if possible

### Recommended PostgreSQL Settings

```
max_connections = 300 shared_buffers = 1GB                # increase based on db and RAM size 
temp_buffers = 1GB  # increase based on db and RAM size 
max_prepared_transactions = 0 
work_mem = 4MB 
maintenance_work_mem = 512MB
effective_io_concurrency = 4     
wal_level = archive    # allows PITR and restore 
fsync = on   # setting it to off can boost performance at the risk of full db corruption
synchronous_commit = on  # can be safely set to off full_page_writes = on
```

Also visit https://pgtune.leopard.in.ua/ for PGTune recommended values based on specific hardware inputs

### Recommended MySQL Settings

```
character-set-server=utf8
default-character-set=utf8
default-storage-engine=INNODB
max_connections=800

# 0 = log and flush once per second, set sync_binlog=2 # 2 = log on commit and flush once per second, set sync_binlog=2 
innodb_flush_log_at_trx_commit=1  
sync_binlog=1  

# increase based on db size and RAM 
innodb_buffer_pool_size=1G 
tx_isolation=READ-COMMITTED
binlog-format=ROW  
tmp_table_size=64M 
innodb_log_file_size=500M 
max_allowed_packet=4M  
innodb_thread_concurrency=10 # make buffer pool instances roughly equal the size of the pool in GB's e.g. for an 8GB pool use: #innodb_buffer_pool_instances=8 

# disable query cache 
query_cache_size=0 
query_cache_type=0 
thread_cache_size=10
```

### MySQL issue with adding indexes / restoring database
Possible error when restoring / importing a MySQL DB:<br>
`ERROR 1118 (42000) at line 2075: Row size too large (> 8126). Changing some columns to TEXT or BLOB may help. In current row format, BLOB prefix of 0 bytes is stored inline.`

Possible error when attempting to add indexes in PaperTrail (or alter table in the DB directly on document_summary_index):<br>
`Caused by: com.mysql.jdbc.exceptions.jdbc4.MySQLSyntaxErrorException: Row size too large. The maximum row size for the used table type, not counting BLOBs, is 8126. This includes storage overhead, check the manual. You have to change some columns to TEXT or BLOBs`

In the my.ini file (Windows - C:\ProgramData\MySQL\MySQL Server 5.7\my.ini) or the my.cnf file (Linux - /etc/mysql/my.cnf), make the following changes in the `[mysqld]` section, and then restart the MySQL service<br>
Increase `innodb_log_file_size=500M`<br>
Add `innodb_strict_mode=0`
