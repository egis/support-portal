# LDAP Configuration  


### Active Directory


* AD will return less results and attributes when using port 3268 vs 389
* The default query will only return accounts with an email address configured

### OpenLDAP 

Configure User format = `uid=${user},o=Directory`

### Multiple LDAP Servers

Configure the first domain in the PaperTrail admin section (Services > Properties > LDAP)<br>
Specify the:<br>
Account Lookup Query: `(&(objectClass=user)(mail=*)(|(displayName=${value}*)(sAMAccountName=${value}*)))`<br>
Domain: `domain01.com`<br>
Host:<br>
Port:<br>
User:<br>
Password:<br>
Verify User:<br>
Check the Skip Verification box<br>

In the papertrail.properties file, add the following for each domain (including the domain specified in the admin section)

Configured by addition a set of properties per domain:

```javascript
ldap.extra.domain01.com.host=
ldap.extra.domain01.com.port=
ldap.extra.domain01.com.username=
ldap.extra.domain01.com.password=

ldap.extra.domain02.com.host=
ldap.extra.domain02.com.port=
ldap.extra.domain02.com.username=
ldap.extra.domain02.com.password=
```

Restart the PaperTrail service for the changes to take affect.

When adding Active Directory users, select `domain01.com` / `domain02.com` from the Domain drop-down list.

## Synchronizing With LDAP / Active Directory

*  Check **LDAP** -> **Auto Create Users**  to create new users from LDAP when they login  
*  Check **LDAP** -> **Auto Sync Groups**  to synchronize group membership, this will sync on user create and on the interval specified under **Authentication** -> **Group Sync Interval**  

You can also specify a datasource under **Authentication -> Group Sync Provider** e.g. `ds:groups`

```sql
SELECT memberOf as groups FROM '@ldap/objectClass=user&SAMAccountName=${filter}
```

## Troubleshooting

*   Get the LDAP queries that PaperTrail is executing by increasing the log level:  `com.egis.utils.ldap` in < 8.8.4 or `com.egis.security.ldap` in 8.8.4+

*  DEBUG to see the results of queries  
*  TRACE to see the actual query being run and authentication requests  
*  Use an off the shelf tool to check what options work when connecting:

GUI:  

[http://jxplorer.org/](http://jxplorer.org/)  
[http://www.ldapsoft.com/ldapbrowser/ldapadmintool.html](http://www.ldapsoft.com/ldapbrowser/ldapadmintool.html)  

CLI:  

```shell
ldapsearch -h 172.16.237.131 -D "administrator@corp.egis-software.com" -w password -b "cn=users,dc=corp,dc=egis-software,dc=com" -s sub "(&(objectClass=user)(mail=*))" '*'
```  

Use tcpdump or wireshark to capture ldap queries and results at the protocol level.  

*   Adjust the LDAP query string in `Services -> Properties -> LDAP` as appropriate
