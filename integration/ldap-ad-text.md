# LDAP Configuration  

### OpenLDAP 

Configure User format = uid=${user},o=Directory

Note: Active directory will return less results and attributes when using port 3268 vs 389

### Multiple LDAP Servers

Configured by addition a set of properties per domain:

```javascript
ldap.extra.**_domain1-corp.local_**.host=  
ldap.extra.domain1-corp.local.user=  
ldap.extra.domain1-corp.local.pass=  
ldap.extra._**domain2-corp.local**_.host=  
ldap.extra.domain2-corp.local.user=  
ldap.extra.domain2-corp.local.pass=  
```

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

*   Adjust the LDAP query string in _Services -> Properties -> LDAP_ as appropriate
