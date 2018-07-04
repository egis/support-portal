## Maintenance Mode
> Setting maintenance mode is essential when conducting upgrades as it will ensure that no new documents/emails are imported after the upgrade is completed, as when a rollback is necessary, the imported documents will no longer be available in watched mailbox. 

### Turning On Maintenance Mode: 
1. Configure papertrail to start in maintenance mode by adding the following line to the `conf/papertrail.properties`
```
mode=Maintenance
```
2. Restart PaperTrail

### Turning Off Maintenance
1. Remove or comment out the **mode** property in `conf/papertrail.properties`
1. Restart PaperTrail
