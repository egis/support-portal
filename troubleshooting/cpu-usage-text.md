# Troubleshooting High CPU usage

## Before doing anything else


Before restarting PaperTrail always try and get a snapshot:

`http://localhost:8080/snapshot`  

and/or a thread dump  

`http://localhost:8080/snapshot/threads`

If the web interface is unresponsive, use the command line to retrieve a
thread dump.

On Linux: `/etc/init.d/papertrail heap`  
On Windows: In <Java Bin Directory>,  Run `jps` to get the PID of the service and then `jstack -dump:format=b,file=C:\heap.bin  <PID>`

## Common Causes of high CPU usage

If a single CPU core is at 100%, the culprit would normally be single thread that reoccurs in every single thread dump.

If all CPU cores are at 100% or near 100%, the cause is either:

a) memory exhaustion - very little free memory,  `jstat`  would return
very high garbage collection times (GC)  
b) an endless loop  
c) too many worker threads and/or too few cores
  

## Analyzing a Thread Dump

Analyzing a thread dump involves looking through all the threads on the
running system to identify a pattern.

*  Any thread in a `TIMED_WAITING` or `WAITING` state can be safely ignored
as these threads are sleeping waiting for something else to occur.

*  Jetty threads in the `java.net.SocketInputStream.socketRead RUNNING `state can also be ignored as they are waiting for a client to make a TCP/IP connection
  

