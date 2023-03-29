# Email Watch

## Import emails from a specific email account
1.  Add a new **Import Management -> Email Account**.  
1.  Add a new **Import Management -> Email Import**.  
1.  **Name** – Specify the name of the import - this will be recorded under the history tab.  
1.  Select the **Node** to import the document into.  
1.  Select the **Account** created in step 1.  
1.  Select an **Attachment** Policy  
		*  _Body Only_ - Import the .html or .txt email body only.  
		*  _Attachments Only_ – Import attachments only e.g .pdf, .word.  
		*  _Source Only_ - Import the email as a .eml suitable for search an preview.  
		*  _Document Archive_ – Used in conjunction with the autoExport rule.  
		*  _Threads_ – Update the original email with any replies – The Document.response event can be used to trigger notifications / workflows etc.
1.  Click Add.


## Filter spam or unwanted messages out
1.  Create one or more **Email Imports** with a Rule Order of 1.  
2.  Specify unwanted terms under the **Field** Tab e.g.  
3.  Create all other **Email Imports** with a Rule Order larger than 1.  

## Import emails from one email account with multiple aliases

1.  Create one **email account**.  
2.  Create one or more email import and specify the alias under the **Rules -> To** and **Rules -> CC** fields.  
3.  Select the **email account** created under step 1.  

## Map email fields to document indexes

1.  Select the **node to import the emails to**.
2.  Map the **fields** under the **Fields** tab.

## Exclude signature images and other attachments from being imported.

1.  Under the **rules** tab, specify a semi-colon separated list of **unwanted extensions** under Attachment Exclusion Filter.
e.g. *.gif;*.jpeg;*.png


OR


2.  Specify only the attachments you want to import under **Attachment Inclusion Filter**.
*.pdf;*.doc*

Update the original email when a reply is received (threading)

## Import emails from Office365 OAuth - Delegated Access

To set up:<br>
URL = https://login.microsoftonline.com/<br>
Add username<br>
Add password<br>
Add the tenantId in Advanced<br>
Add the clientId in Advanced<br>
Add the resource in Advanced<br>

e.g. in Advanced:<br>
```properties
tenantId=12345
clientId=abcde
resource=EWS.AccessAsUser.All
```


## Import emails from Office365 OAuth - Application Access

### To set up:
URL = `https://login.microsoftonline.com/`  
Add User Email as `username`  
Add Client Secret as `password`  
Add the `tenantId` in Advanced  
Add the `clientId` in Advanced  
Add the `resource` in Advanced  
Add the `secret=true` in Advance

e.g. in Advanced:<br>
```properties
tenantId=12345
clientId=abcde
resource=https://outlook.office.com/.default
secret=true
```

## Troubleshooting email imports:

1.  Ensure that standard email clients can connect over the POP and IMAP Protocols.
2.  Check **Services -> Properties -> Imports -> Debug POP/IMAP** to record the conversion with the POP/IMAP server to if it returns any error messages.

## Polling mail servers with a self-signed certificate
Should you not be able to connect to a mailbox, with the below error in the logfile, the issue is due to a certificate not in the Java cacerts file:<br>
`PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target`

1. Obtain a copy of the CER file for the mailserver and save on disk to the PaperTrail server (mailserver.cer in this example)
2. Run CMD prompt as administrator / Linux shell as root
3. Navigate to the Java bin directory:<br>
 - Windows: `C:\Program Files\Java\jre1.8.0_221\bin`<br>
 - Linux: `/usr/lib/jvm/java-8-oracle/jre/bin`<br>
4. Import the certificate to the Java Security cacerts file<br>
 - Windows: `keytool -importcert -trustcacerts -file "C:\Downloads\mailserver.cer" -keystore "C:\Program Files\Java\jre1.8.0_221\lib\security\cacerts" -alias "mailserver"`<br>
 - Linux: `keytool -importcert -trustcacerts -file /root/mailserver.cer -keystore /usr/lib/jvm/java-8-oracle/jre/lib/security/cacerts -alias mailserver`<br>
5. Set the password to `changeit` and trust the certificate
6. Restart PaperTrail
7. If there is still an issue, try adding this line to run.sh / service_x64.vmoptions and restart PaperTrail<br>
 - Windows `-Djavax.net.ssl.trustStore=C:\Program Files\Java\jre1.8.0_221\lib\security\cacerts`<br>
 - Linux `-Djavax.net.ssl.trustStore=/usr/lib/jvm/java-8-oracle/jre/lib/security/cacerts`<br>

## Issues polling mail servers with TLS
Should you not be able to connect to a mailbox, with the below error in the logfile, the issue is due to a Java update which disables legacy TLS protocols:<br>
`Failed to connect to: mailbox@outlook.office365.com:993 javax.mail.MessagingException: No appropriate protocol (protocol is disabled or cipher suites are inappropriate); nested exception is: javax.net.ssl.SSLHandshakeException: No appropriate protocol (protocol is disabled or cipher suites are inappropriate)`

It appears that a release of Java around April 2021 disables TLSv1 and TLSv1.1.
The below lines in the java.security file (\Java\jre1.8.0_291\lib\security) should be commented out and PaperTrail restarted:<br>
`#jdk.tls.disabledAlgorithms=SSLv3, TLSv1, TLSv1.1, RC4, DES, MD5withRSA, \`<br>
`#    DH keySize < 1024, EC keySize < 224, 3DES_EDE_CBC, anon, NULL, \`<br>
`#    include jdk.disabled.namedCurves`

## Issues with *Remote host closed connection during handshake*
Should you not be able to connect to a mailbox, with the below error in the logfile, the issue is due to an outdated mail.jar file in the PaperTrail libs directory<br>
`Failed to connect to: mailbox@mail.com@mailserver:993 javax.mail.MessagingException: Remote host closed connection during handshake;`

The offending mail.jar is v1.4.4, with the updated jar being v1.6.2

1. Remove `mail.jar` from the libs directory
2. Obtain v1.6.2 of `javax.mail.jar`, rename to `mail.jar` and place in the libs directory (https://javaee.github.io/javamail/#Download_JavaMail_Release)
3. Restart PaperTrail

See also PPT-11861

## Polling email servers via a Proxy
Should PaperTrail be forced to use a proxy server for outside connectivity, PaperTrail 889 b2479 onward is required with the below settings:<br>
`mail.ewsstore.proxy.host=myproxyhost` (proxy host - required)<br>
`mail.ewsstore.proxy.port=80` (proxy port - required)<br>
If the proxy requires authentication, the following settings are required:<br>
`mail.ewsstore.proxy.user=myuser`<br>
`mail.ewsstore.proxy.password=mypassword`<br>

Note that these proxy settings are specific to email imports and differ from the general proxy settings needed to reach, for example, SMS gateways
