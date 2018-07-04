# Logging

## Updating the log settings

*  All log settings are stored in the `conf/logback.groovy` file.  
*  The _Admin -> Services -> Logging_  page will make changes to this file if the After Restart option is selected.

## Loggers


| Logger        | Description  | Verbosity
| ------------- |-------------  | ----------
| com.egis.index   | Info about updates to the search index | 10+ lines per doc update
| com.egis.index.query   | SQL and Search index queries | 10+ lines per search
| com.egis.storage   | File operations  | 1+ lines per file read/write
| com.egis.kernel.messaging   | All messages – useful to see what is occurring as a whole | 10+ lines per transaction and/or event
| com.egis.web.WebErrorHandlerImpl  | Show full validation and access denied errors | Full stack on validation or access denied exception
| com.egis.conversion  | Issues with converting files to PDF and Flash | Up to 20+ lines per conversion
| com.egis.web.ActionResource  | All user actions initiated via the UI with params, very verbose | 1 long log line for every user action
| com.egis.DocumentLogger  | All actions on documents, somewhat verbose | Up to 5 - 10 lines per document operation
| com.egis.requests  | All HTTP requests, very verbose | 1 line per HTTP request
| com.egis.workflow  | All Workflow rules fired up until a stationary rule is reached (Human Task, Unassigned Task) | 10+ lines depending on amount of rules
| com.egis.allocation.QueueService | queue fill events | 
| com.egis.party.GroupSyncService  | Group sync job's user group membership actions | 2 lines per user

## Log file Retention

*  To configure the number of days to keep Papertrail logs, locate and edit the following document: `PaperTrail/conf/logback.groovy`
-  The example below keeps the logs for a period of 14 days:
```javascript
appender("FILE", RollingFileAppender) { 
file = "logs/server.log"     
append = true     
rollingPolicy(TimeBasedRollingPolicy) {  
maxHistory = 14  
FileNamePattern = "logs/server-%d{yyyy-MM-dd}.log"
}}
```  
-  Locate the section `maxHistory = 14`. Please modify the 14 with the amount of days to keep logs.  
-  Restart PaperTrail for the settings to take effect.  

## Logging to Syslog Host

```javascript
import com.egis.utils.apm.*; 
import org.productivity.java.syslog4j.impl.net.tcp.*; 
appender("SYSLOG", SyslogAppender) {  
layout(LogglyLayout) {        
apiToken = "XXXXX"     
}     
syslogConfig(TCPNetSyslogConfig) { 
host =  "logs-01.loggly.com"
port = 514
ident = "papertrail"     
} 
}
```

## Filtering logs

e.g  To filter out all sql SELECT statemetns with `db.debug=true`: 

```groovy
import ch.qos.logback.core.filter.*
import ch.qos.logback.classic.boolex.*
import static ch.qos.logback.core.spi.FilterReply.*

appender("STDOUT", ConsoleAppender) {
    filter(EvaluatorFilter) {
      evaluator(GEventEvaluator) {
        expression = 'e.message.toLowerCase().startsWith("select")'
      }
      onMismatch = NEUTRAL
      onMatch = DENY 
    }
    
    // encoder(PatternLayoutEncoder)...

}


```

## Logging to a GELF Host

Replace //gelf in the logback.groovy with:

```javascript
appender("GELF", GelfAppender) { 
host = "${gelfHost}"
filter(ThresholdFilter) { 
level = ${gelfLevel} 
} 
port = 12201 
additionalFields =  '{"threadName": "threadName", "exception": "exception", "loggerName": "loggerName", "ip":"ip","user":"user","doc":"doc"}' 
}
```

The following properties will automate this setup: `gelf.host` and `gelf.level`
