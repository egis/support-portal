# SSO

## SAML Single Sign On

SAML SSO lets a third-party service (an identify provider) authenticate users. A user is authenticated on an identity provider’s website.   

The identity provider redirects the user to the PaperTrail website and sends PaperTrail a SAML token. PaperTrail validates the SAML token and logs the user in. The user does not enter a username or a password.  

From __Services →Properties →SSO (SAML)__, select these fields:  

*  __Public Key:__ The name of the identity provider’s public key. The public key is in the conf directory in the installation folder.  
*  __Private Key:__ If encryption is used for the SAML token, enter the path to the private key.  
*  __Identity Provider URL:__ The URL of the identity provider endpoint.  
*  __Login Mapping:__ The element in the SAML token that maps to the login name in PaperTrail. Usually, the element is NameID.  

To make all authentication use SAML, change the **Services→Properties→Front End→Main Page property** to */saml*.  

## Windows Based SSO (NTLM)

NTLM SSO allows for users to be logged in automatically if they are already logged onto their domain account on their PC.   

Check __Services → Properties → SSO__ (Windows Kerberos/NTLM)

### Windows Based SSO (NTLM): Automatic Logon settings
If SSO is not functioning as expected (e.g. the browser displays a Windows Security authentication window prompting for credentials), check the settings in Internet Explorer around Automatic Logon:

* Ensure that the Custom-level Security Setting for User Authentication is set to `Automatic log-on only in Intranet zone`
* Add the hostname and IP address of the PaperTrail server to the `Local intranet zone`

**Note:** The Google Chrome browser uses the security settings around SSO from those defined in Internet Explorer.

## Linux Based SSO (Kerberos) 

Sometimes PaperTrail is installed on Linux server but needs to login in users automatically via Active Directory – This is only possible by using native Kerberos

*  Add the server (e.g., papertrail-srv) to the **AD Domain** (e.g., ad.local)  
*  Create a **user account** (e.g., papertrail-acc) on the AD Domain  
*  Configure PaperTrail to **run as the user account** (e.g., papertrail-acc)  
*  Create a **SPN for each path** that PaperTrail will be accessed by. 
```javascript
e.g., for port 80:
setspn.exe -A HTTP/papertrail-srv papertrail-acc
setspn.exe -A HTTP/papertrail-srv.ad.local papertrail-acc
e.g., for port 8080:
setspn.exe -A HTTP/papertrail-srv:8080 papertrail-acc
setspn.exe -A HTTP/papertrail-srv.ad.local:8080 papertrail-acc
```

*  Enable SSO on PaperTrail by editing the __Services → Properties → SSO (Kerberos)__ properties.
```javascript
Enable: ticked
Domain: ad.local
KDC: kdc.ad.local (whichever server responds to "ping ad.local" should be listed here)
Username: papertrail-acc
Principal: papertrail-acc
Password: {password for papertrail-acc}
```

*  Update the **Front End → Index Page** to: **/web/webapps/main.html**.
*  Users need to be **logged onto the domain** (ad.local) and access **PaperTrail via the FQDN** (e.g., papertrail-srv.ad.local)

