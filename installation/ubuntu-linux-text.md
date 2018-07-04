# Ubuntu Linux

## Java

*  Install Oracle Java 8 SDK:
```shell
add-apt-repository ppa:webupd8team/java --yes   
apt-get update   
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
apt-get install oracle-java8-installer update-java-alternatives -s java-8-oracle  
```

*  Install JCE Unlimited strength policy files for some AES-256 encryption operations (optional).

*  The policy jar files can be downloaded from [here](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)
```shell
cp local_policy.jar /usr/lib/jvm/java-8-oracle/jre/lib/security/
cp US_export_policy.jar /usr/lib/jvm/java-8-oracle/jre/lib/security/ 
```


## PostgreSQL 

*  Install PostGres 

```shell
apt-get install postgresql-9.3
```

(If postgres is not available, follow the instructions at http://wiki.postgresql.org/wiki/Apt to install the repository and then re-try.)

*  Create database and postgres Papertrail user:

```shell
PSQL_VERSION=9.3 sudo -u postgres psql -c 
"CREATE ROLE papertrail PASSWORD 'papertrail' SUPERUSER CREATEDB CREATEROLE INHERIT LOGIN;"   
sudo -u postgres psql -c 'create database papertrail with owner papertrail;'  
echo host  papertrail papertrail  127.0.0.1/32 md5 >> /etc/postgresql/$PSQL_VERSION/main/pg_hba.conf /etc/init.d/postgresql restart
```

### Setup PostgreSQL to allow remote connections
This is useful if you wish to install PaperTrail on a Windows server for example, but wish to keep the PostgreSQL DB on a Linux environment. Following the below will allow the Windows host to communicate with the Linux DB host and also allow you to use the pgAdmin GUI and tools against the Linux DB.

1) On the Linux machine hosting the PostGres DB, navigate to `/etc/postgresql/[version]/main/`

2) Modify file `pg_hba.conf` to add entries under IPv4 local connections for each host; e.g  
`host    all             all             127.0.0.1/32            md5`  
`host    all             all             192.168.192.10/32       md5`

3) Modify file `postgresql.conf` and unhash the listen_addresses, changing it to  
`enable listen_addresses = '*'`

4) Restart the postgresql service  
`service postgresql restart`

## Conversion

Install the following dependencies:

*  libreoffice
*  libtiff-tools
*  ghostscript
*  swftools

```shell
apt-get install libreoffice libtiff-tools ghostscript
```

swftools is not a standard package - To install it, use
```shell
sudo apt-get -y install libjpeg62 libgif4 sudo apt-get -y install libart-2.0-2 wget -P /tmp/http://archive.canonical.com/ubuntu/pool/partner/s/swftools/swftools_0.9.0-0ubuntu2_amd64.deb chmod a+x /tmp/swftools_0.9.0-0ubuntu2_amd64.deb sudo dpkg -i /tmp/swftools_0.9.0-0ubuntu2_amd64.deb
```

## PaperTrail Service

1) Install PaperTrail
`sh Papertrail_<version>.sh -q`

2) Update the db settings in the `/opt/Papertrail/conf/papertrail/properties`

```javascript
db.database=papertrail
db.host=localhost
db.pass=papertrail
db.user=papertrail
db.type=postgresql
```

3) Start papertrail
`/etc/init.d/papertrail start`

### Troubleshooting the PaperTrail Service
Occasionally, the PaperTrail service may fail to stop. While `service papertrail status` may show that the service is inactive, the java process could still be running. In this scenario, you'll see that the PaperTrail web front-end is still available. Executing `ps -aux` will show the java process still running.

1) To end the java process: `killall java`
2) Verify that the PaperTrail web front-end is down. If this is still up, try `killall -KILL java` to end a stubborn java process.  
**Note:**  
`killall java` - will do a controlled shutdown  
`killall -KILL java` - just terminates the process, which can cause PaperTrail to lose messages
