# Messaging

![](http://i.imgur.com/x9IVpdW.png)  

## Managing Message Queues

To clear / restart message queues:  

*  Navigate to __Services->Messaging__. Select the __message queue__ and
*  Click __Reprocess Failed/Dead__ to reprocess messages.  
*  Click __Clear All__ to clear any messages out of the queue.  

> WARNING: this may produce unexpected results e.g. partial email delivery, failed conversions not being retried etc.

| Queue | Description 
| -------- | ---------
| IndexUpdate.replicate | Index replications queue
| IndexUpdater.update | Updates to the search indexes
| EmailNotifierImpl.sendQueued | Queued email messages
| Rule.generatePdf | Office -> PDF and Flash conversions
| Rule.* | Any asynchronous rule invocation
| replicate | Data replication
| <store>.write | File replications and online cloud backups
