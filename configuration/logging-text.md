#Logging

## Updating the log settings

*  All log settings are stored in the `conf/logback.groovy` file 
*  The _Admin -\> Services -\> Logging_  page will make changes to this file
if the After Restart  option is selected


## Log file Retention 

*  To configure the number of days to keep Papertrail logs, locate and
    edit the following document: `PaperTrail/conf/logback.groovy`
e.g. keeps the logs for a period of 14 days:
```groovy
appender("FILE", RollingFileAppender) {             
	file = "logs/server.log"             
	append = true             
	rollingPolicy(TimeBasedRollingPolicy) {                 
		maxHistory = 14                 
		FileNamePattern = "logs/server-%d{yyyy-MM-dd}.log"             
	}         
}
```

*  Locate the section `maxHistory = 14`  modify the 14 with
    the amount of days to keep logs.
*  Restart PaperTrail for the settings to take effect.


## Logging to Syslog Host

```
import com.egis.utils.apm.*; 
import org.productivity.java.syslog4j.impl.net.tcp.*; 

 appender("SYSLOG", SyslogAppender) {  
    layout(LogglyLayout) {     apiToken = "XXXXX"     }    
    syslogConfig(TCPNetSyslogConfig) {     
    	host =  "logs-01.loggly.com"
		port = 514
		ident = "papertrail"
    } 
}
```

## Logging to a GELF Host 

Replace //gelf in the logback.groovy with:

```
appender("GELF", GelfAppender) {     
	host = "${gelfHost}"    
 	filter(ThresholdFilter) {       
   		level = ${gelfLevel}   
   }    
   port = 12201  
   additionalFields =  '{"threadName": "threadName", "exception": "exception", "loggerName": "loggerName", "ip":"ip","user":"user","doc":"doc"}' 
}
```

The following properties will automate this
setup: `gelf.host` and `gelf.level`


## Logging to individual files per logger
 e.g. to append file access logs to a standalone `storage.log` file:

```
appender("STORAGE", RollingFileAppender) {
    file = "logs/storage.log"
    append = true
    rollingPolicy(TimeBasedRollingPolicy) {
        maxHistory = 14
        FileNamePattern = "logs/storahe-%d{yyyy-MM-dd}.log"
    }
    encoder(PatternLayoutEncoder) {
        pattern = "%d{HH:mm:ss.SSS} %level %logger{0} [%X{user}%X{doc}:%X{ip}] %msg%n"
    }
}


logger('com.egis.storage', INFO)
logger("com.egis.storage", DEBUG, ['STORAGE'], false)
```

