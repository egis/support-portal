# Exceptions 

## System cannot find the file specified

`java.io.IOException: Cannot run program "pg\_dump": CreateProcess
error=2`  
Reason : The system cannot find the file specified  
Solution : Add the Postgresql/bin directory to the System PATH environment variable

## System cannot find the file specified

`java.io.IOException: Cannot run program "mysql\_dump"`  
Reason : The system cannot find the file specified  
Solution : Add the MySQL/bin directory to the System PATH environment variable
  
## Database connection Pool exhausted

`JDBCExceptionReporter [:] Cannot get a connection, pool error Timeout
waiting for idle object Database connection pool is exhausted,`  

Solution :   
-  Check for database connection leak warning messages in the log files
beforehand  
-  Check database lookup configurations  
  
## Permission denied

`failed <SocketConnector@0.0.0.0>:80:
[java.net](http://java.net/).BindException: Permission denied`

Solution : To run PaperTrail on port 80 you need to be root, change http.port=8080
  
