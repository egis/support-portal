## Security Mode

PaperTrail can be run in 4 distinct security modes under **Properties -> Security -> Security Mode**

###  Low (Default)

Suitable for intra-net based deployments without confidential data 

### Medium


Access to the various API's used for replication and clustering is
restricted based on Trusted Server entries, some of the endpoints
restricted include:
  

-   conversion
-   signature/upload
-   index/replication
-   store
-   replicate

### High 

Includes all the restrictions of Medium and:
  

-   disables the /script/console endpoint (used by
    /web/admin/console.html and pt script CLI)
-   prevents updates to the following properties via the web UI, they
    need to be set via papertrail.properties file:

 
```javascript
    ldap.host  
    waffle.enable  
    spnego.enable  
    spnego.kdc  
    smtp.debug  
    email.spool  
    smtp.host  
    sms.url  
    web.login.sms.otp  
    index.store  
    http.ssl  
    disabled.audits  
    disabled.entity.audits  
    openoffice.path  
    tiff2pdf.process  
    pdf2swf.process  
    security.level  
```

### Very High

 Includes all the restrictions of High and further restricts:

-   Loading jar files via System/jars folder
-   Loading scripts via System/scripts folder
-   Loading UI plugins via System/plugins folder
-   Scripted data sources
-   runScript, dbLookup and commandLineProcess rules
-   Custom options in Meta Model Fields
-   PQL Expressions




## Brute Force Login protection

There are 2 options under Properties -> Authentication that can be enabled

`Captcha on password reset` - Force a captcha to be passed before allowing a password reset email to be sent  
> Tip: password resets can also be disabled by unchecking `enable self service password reset`
`Captcha on login attempts` - Force a captcha to be passed before X number of failed login attempts



## Brute Force Request Protection

Check `Enable brute force protection` under `Services -> Security`  

## Secure Cookie Handling

Check the options under `Services -> Security -> Cookies`

## API Monitoring:

- Monitoring MUST be enabled for this to work

API monitoring Events:

```
api-write
api-read
api-misuse
```

###### api-write
 
 Will increment on each of the following:
 
	1. upload
	2. update
	3. update metadata
	4. delete
	5. node create

###### api-read

Will increment on each of the following

	1. read/open document

###### api-misuse

Will increment and log when API module is not enabled and some default resource is used.

`WARN  LicenseFilter [:Administrator:0:0:0:0:0:0:0:1] Possible API misuse detected: /document/details/94`

The above warns of possible misuse as well as the resource path.

### Notifications:

Under `Admin > Services > Monitoring`

Notifications can be set up that will email support when an event reaches a threshold in a certain period. For example: email support when `api-misuse` event reaches 10 events in 5 days.
