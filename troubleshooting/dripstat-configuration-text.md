# Dripstat Configuration

Dripstat monitoring can be installed and configured on PaperTrail instances to monitor performance and enable more detailed information relating to server/web service performance issues.

The following will need to be set up:

1. Download the Dripstat JAR file from https://s3.amazonaws.com/papertrail/libs/dripstat.jar 
2. Copy the JAR to PaperTrail installation path/dripstat
3. Copy the config.properties file (only generated once a license has been purchased) to PaperTrail installation path/dripstat
4. Add the following line to the service.vmoptions OR service_x64.vmoptions:
<br>
   -javaagent:dripstat/dripstat.jar
5. Restart PaperTrail and confirm that dripstat has started correctly via the PaperTrail log files. The server/application performance details will be available via the Dripstat monitoring website once PaperTrail has started with Dripstat configured.
