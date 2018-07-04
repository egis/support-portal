### Configuring service settings 
  

| OS        | Configuration Applied in
| ------------- |-------------
| Linux   | /opt/Papertrail/run.sh 
| Windows | service.vmoptions / service_x64.vmoptions

###  Configuration Options 

| Option        | Description | Example
| ------------- |------------ | -------
| -Xmx    | Max memory | -Xmx2048M
| -Xms    | Min memory | -Xms2048M
| -Xss    | Thread Stack Size | -Xss1m

### System Properties

System properties can be set via different sources, in the following resolution order:  
1) Runtime  
2) Database  
3) File (in `conf/papertrail.properties`)  
4) Startup Argument

## Runtime
System properties can be viewed and changed *on the fly* in a running environment by executing the following runtime commands from the PaperTrail Console:  
`System.getProperty('systemProperty')` to view a property's value  
`System.setProperty('systemProperty', 'value')` to set a property's value  
e.g. `System.setProperty('sampleproperty', 'true')`

## Database
Example below given for a PostgreSQL DB:  
`update system_property set value = 'SampleLicenseText' where name ='license'`

## File or Startup Argument
System properties can either be set as startup configuration option using `-DsystemProperty=value`, or in the `conf/papertrail.properties` file:

| System Property | Description | Example
| ----------------| ------------| -------
| java.net.useSystemProxies||true
| http.proxyHost|HTTP Proxy Host|squid
| http.proxyPort|HTTP Proxy Port|8800
| http.proxyUser|    |
| http.proxyPassword|     |
| http.nonProxyHosts|    |`localhost / 127.0.0.1 / 10.*.*.* / *.foo.co` etc
| socksProxyHost|     |
| socksProxyPort|     |
| java.net.socks.username|     |
| java.net.socks.password|   | 

