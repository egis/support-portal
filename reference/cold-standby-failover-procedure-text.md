# Cold Standby Failover Procedure

*  Ensure the master server is actually down and not immediately recoverable.  
*  Kill the master server i.e. ensure that the primary server does not continue to operate (service requests) as it could cause missing data or conflicts down the line - If necessary, physically remove network cables.  
*  Run the `C:\failover.bat` script which automates the following actions:  
		-  Stop PaperTrail.  
		-  Delete the existing properties file: `C:\Program Files\Papertrail\conf\papertrail.properties`.  
		- Copy and rename the `C:\failover.properties` to: `C:\Program Files\Papertrail\conf\papertrail.properties`.  
		- Start PaperTrail.  
		- Repair the indexes.  

## Failover Verification Procedure

*  Confirm new documents can be imported.  
*  Confirm old documents can be viewed.  
*  Confirm documents are searchable by running an index repair.  
*  Confirm all file and email imports functioning (if applicable).  
*  Confirm file store integrity by running file store repair.  

## Client / Imports Failover Procedure

Note :  **DO NOT COMPLETE THE FOLLOWING STEPS DURING DR TEST.**

*  Move or change the IP / hostname from the master to the slave so that users can connect to PT as normal.  
*  Rename the server for all file and email imports.
e.g. `UPDATE import_setting SET serverId = <id of slave server>`
*  Restart email and import file services.