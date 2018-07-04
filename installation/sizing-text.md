## PaperTrail Server Requirements

-    2 - 4GB RAM
-   2 Modern CPU Cores
-   20GB + free disk space

### Database

*  The database should be kept entirely in RAM on fast disks (SSD, RAID 1
with cache etc). A rough guideline is to use 1GB of RAM per 1 million docs.  
*  A centralized database can be used, however it can introduce latency.  

### Index Directory

*  The index directory is where Lucene stores all indexes for searching. As
a rule of thumb is it's around 1 - 2 GB per million docs, more if full
text searching is enabled.  
*  The index directory needs to be on fast disks (RAID 0, SSD) and does
not need to backed up as it can be easily and quickly (with full text
disabled) rebuilt.  

###  File Repository

*  The file repository has lots of small file based IO where each file is stored
by name as checksum. So once a file is written, it is never updated - only
deleted.
*  It can safely be backed up and then archived.
*  RAID 6+ is sufficient.
*  Files can also be stored on a object storage platform like Amazon S3,
Caringo CAStore reducing the need for backups.
*  Replication can also be configured between 2 PaperTrail instances using
file stores.
  

