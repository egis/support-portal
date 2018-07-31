<b>Replication installation on new instance of PaperTrail:</b>

Install PaperTrail onto both Master and Slave with Replication turned off (do not add the Replication configuration to the papertrail.properties file). 

Make sure all deployment files deploy correctly and that PaperTrail is accessible via the front end.

Log in with the Admin user and set the same password on both instances

Shut down PaperTrail on both instances

Configure Replication Settings in papertrail.properties file on both Master and Slave:

<b>Master:</b>

index.upstream=http://slave:8080<br>
replication.upstream=http://slave:8080<br>
file.replication.upstream=http://slave:8080<br>
replication.master=true<br>
replication.increment=2<br>
replication.offset=1<br>

<b>Slave:</b>

index.upstream=http://master:8080<br>
replication.upstream=http://master:8080<br>
file.replication.upstream=http://master:8080<br>
replication.master=false<br>
replication.increment=2<br>
replication.offset=2<br>

Start up PaperTrail on Master server and make sure that PaperTrail starts up without any issues in the logs and that the website is available

Start up PaperTrail on Slave server and make sure that PaperTrail starts up without any issues in the logs and that the website is available
