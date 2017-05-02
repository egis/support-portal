## File Stores


If now file stores are configured papertrail will create an in-memory store based on the value of the **data.dir** property:

*http://* or *https://* - HTTP Store  
*directory location* - File Store  

## Tasks

### Synchronize

Copies from 1 store to another.  
**Sync** - copies and overwrites all files - *not recommended*  
**Repair** - only copies the file if it does not already exist  
**Verify** - ensures that every file checksum is correct, otherwise recopy  

Can also be used to verify the integrity of a store by read / writing to the same store in **Repair** mode.

### Restore

Restores a file repository from backups created using the **Backup** option when create the original store.

### Archive

> WARNING: This will delete files, only run if the files have been backed up to a secondary store e.g. S3

### Check Integrity

Useful for when recovery of a file store has only been partial.

Similar to Synchronize with repair, but will export a CSV log of all missing blobs with the docId associated and optionally updating affected documents 
with `missing_blob=true`


