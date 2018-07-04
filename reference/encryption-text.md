# Encryption 

## Encrypting files at rest (AES)

*  Add the following to the __papertrail.properties__ file before starting PaperTrail for the first time   
`storage.encrypt=true`

OR

*  Add a new file store under __Services -> File Store__.  
*  Select Software under the __Encrypt__ option.  
*  Enter a __Key size__ e.g. 128, 196, 256.  
*  Enter the __unique key name__ for this store.  
*  The __encryption key will be automatically generated__ on restart and stored obfuscated in the database.  

## Encrypting files in transit (SSL)

*  Create a __Java keystore (JKS)__ 

>If you have a pfx or certificate in another format it will need to be converted to JKS using tool like  [KeyStore Explorer](http://keystore-explorer.sourceforge.net/index.php) or [OpenSSL](https://www.digicert.com/ssl-support/jks-import-export-java.htm)

*  Copy the keystore to __conf/keystore__.
*  Under __Services -> Properties -> Front End (SSL)__.
*  Check __Enable__.
*  Enter the __keystore password__.
*  Optional: Check __Force SSL__ to ensure all traffic from HTTP is redirected to HTTPS.  
*  Click __Save__.  
*  Restart __PaperTrail__.  

## Encrypting Outbound Email (SMIME)

In `papertrail.properties` add the following property:
e.g.
```
email.smime.out.<email address>=<path to X509 public certificate>
```
e.g.
```
email.sime.out.confidential@example.com=C:\public.cert
```

To test: Email anything from PaperTrail to that email and it should automatically be encrypted.



## Decrypting Inbound Email (SMIME)

Under `Services -> Properties -> Imports` configure.

**Email Decryption Cert Path**: A path to a JCEKS Key Store  (Note: JCEKS not JKS) that contains one or more keys to decrypt incoming email. The file should have an `jceks` extension. Each entry in the keystore should have the same password as the keystore it self.  

**Email Decryption Password**: The password to the keystore.  

To test try and view any encrypted mail in preview - The body and attachments should be available - if it does not work then a smime.p7m attachment will only be visible.
 

