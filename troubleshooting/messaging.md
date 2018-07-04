# Messaging

PaperTrail implements a message bus for both sync and async message passing. Messaging provide multiple benefits:

* de-couples modules to reduce complexity
* cater for unreliable services to improve stability and reliability 
* provides plugin points to improve configurability
* improves visibility of what the system is doing at any point by logging messages

See [Message Bus](https://msdn.microsoft.com/en-us/library/ms978583.aspx)  and [Message Queue](https://en.wikipedia.org/wiki/Message_queue) 

![](http://i.imgur.com/x9IVpdW.png)  

## Common Message Queues
| Queue | Description 
| -------- | ---------
| IndexUpdate.replicate | Index replications queue
| IndexUpdater.update | Updates to the search indexes
| EmailNotifierImpl.sendQueued | Queued email messages
| Rule.generatePdf | Office -> PDF and Flash conversions
| Rule.* | Any asynchronous rule invocation
| replicate | Data replication
| <store>.write | File replications and online cloud backups

## Properties
| Property                            | Default                   | Description                              |
| ----------------------------------- | ------------------------- | ---------------------------------------- |
| message.retry.check.interval        | 60                        | How often to check for messages eligble for retry (ms) |
| message.retry.max                   | 5                         | Max number of message retries            |
| message.retry.max.**queueId**       |                           |                                          |
| message.retry.intervals             | 60,3600,14400,86400,86400 | Message retry backoff schedule (ms)      |
| message.retry.intervals.**queueId** |                           |                                          |
| message.retry.min.interval          | 10000                     | Minimum period between message retries   |
| message.queue.size                  | 500                       | Size of the in memory queue              |
| message.queue.size.**queueId**      |                           |                                          |
| message.failover.**queueId**        | *None*                    | Failover to this queue instead of marking as dead |
| message.threads.**queueId**         |1                          |  Increase the concurrency of the queue to use more threads to process messages|

Message queues and properties are set using the **queueId**, normally `ClassName.methodName` - 1 event could have multiple queue's each with their own settings 

`message.queue.size` and `message.queue.size.{queueId}` define the size of the in memory queue, attempts to append messages to a full queue will result in them being persisted instead. 

## Persistence
Messaging persistence always occurs within the context of a database transaction. i.e. A message will not be triggered if the database transaction fails.  
However if the message fails, the queue handler will attempt to persist to database - should that persistence fail, then the message will be lost unless journalling is enabled.

### Journalling

Messaging journalling uses a seperate persistence store, other than the DB i.e. it will survive a database persistence failure.  
The default maessage journal is based on LevelDB - Before anything happens with a message it will be saved to LevelDB, only once the message is succesfully processed or persisted to db
will it be removed from LevelDB.

On startup leveldb is checked for any messages needing recovery and they are then immediatly persisted. 

## Timeouts

Message processing timeouts can be specified using `@Timeout` if the running time of processing the message exceeds this limit, then the thread is interruppted and then the message is marked as failed and persisted for retry. The thread

## Retry's

Persisted messages are periodically checked for retriability and then placed back on the queue - the backoff period is specifed using the **retry.intervals**

Once the max number of retries have occured the message is marked as dead and will not be retried.

## Failover

If a failover queue is specifed than instead of marking a message as dead, it will be moved to a new queue with a new retry schedule.

## Managing Message Queues

To clear / restart message queues:  

*  Navigate to __Services->Messaging__. Select the __message queue__ and
*  Click __Reprocess Failed/Dead__ to reprocess messages.  
*  Click __Clear All__ to clear any messages out of the queue.  

> WARNING: this may produce unexpected results e.g. partial email delivery, failed conversions not being retried etc.


