# Configuring HTTPS (Server Side Only)

To configure PaperTrail to use HTTPS:

1. Create a Java key store (JKS) with a name of `keystore` and place it in the `conf` directory
2. Specify the keystore password via `http.ssl.password`
3. Check Properties -> HTTPS -> Enable (`http.ssl`) to true
4. Set the HTTPS port (`http.ssl.port`) to 443 or 8443
5. Check Force SSL (`http.ssl.force`) to always redirect from HTTP to HTTPS

### TIP: Portecle is a useful app to work with certificates.


## Converting PKCS#7 to PKCS#12

`openssl pkcs12 -export -in server.crt -inkey server.key   -out keystore.p12 -name www`
               
## Converting PKCS#12 to JKS

`keytool -importkeystore -destkeystore keystore -srckeystore keystore.p12 -srcstoretype PKCS12`               


### Import Root and Intermediate CA's

`keytool -import -trustcacerts -alias root -file root.crt -keystore keystore`


### Verifying
To verify that the keystore is configured correctly:

`keytool -list -keystore keystore` 

Which should produce something like:

>Keystore type: JKS
>Keystore provider: SUN
>
>Your keystore contains 1 entry
>
>*.papertrail.co.za, Oct 29, 2015, PrivateKeyEntry, 

The last line has a syntax of `{CN} {Expiry} {Key Type}`  

`{CN}` should match the URL you would be accessing PaperTrail by  
`{Key Type}` must be PrivateKeyEntry  

# Configuring Client Authentication (Mutual SSL)

1. Configure server side SSL as above
2. Create a new a JKS file called `truststore` containing the trusted CA's
3. Check Require Client Certificates (`http.ssl.client.require`)

Configuring client certificates requires that **all** clients supply a trusted certificate.

The Common Name (`CN`) of the certificate will be used to map the a certificate to a user via the login field.
