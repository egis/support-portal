# User export and import via the pt CLI command

### Requirements
* Ensure that the `pt` utility is installed on a Linux host. See guide [here](../installation/cli-article.md)

### Export current user database
* From the Linux host, execute<br>
`pt --host 192.168.1.10:8080 --username admin --password 'mypassword' export User > users.yml`
* Evaluate the contents of users.yml to identify the required fields; example below:<br>
`--- !<User>`<br>
`active: true`<br>
`email: egis1@testserver.com`<br>
`login: egis1`<br>
`name: Egis1`<br>
`properties: {otp: 'false'}`<br>
`userType: FULL`

### Capture new user information
* Create a csv file with details of the new user accounts to be imported; example cell structure below (remember to convert this to csv):

| active | email                | login | name       | properties     | userType |
| ------ | -------------------- | ----- | ---------- | -------------- | -------- |
| true   | gillb@testserver.com | gillb | Gill Bates | {otp: 'false'} | FULL     |
| true   | joes@testserver.com  | joes  | Joe Soap   | {otp: 'false'} | FULL     |

* Convert the csv data to YAML. There is a decent online converter [here](http://www.becsv.com/csv-yaml.php)

* Your YAML output should look like the below:<br>
`---`<br>
`-`<br>
`    active: true`<br>
`    email: gillb@testserver.com`<br>
`    login: gillb`<br>
`    name: Gill Bates`<br>
`    properties: {otp: 'false'}`<br>
`    userType: FULL`<br>
`-`<br>
`    active: true`<br>
`    email: joes@testserver.com`<br>
`    login: joes`<br>
`    name: Joe Soap`<br>
`    properties: {otp: 'false'}`<br>
`    userType: FULL`<br>

* Remove the first line `---`
* Perform a simple find-and-replace to substitute `-` with `--- !<User>` and your YAML file should now resemble the output from the earlier user database export
* Ensure that there are no duplicate login values and no illegal characters in any of the fields

### Import new user database
* Copy your YAML file over to the Linux host (using WinSCP as an option)
* On the Linux host, execute<br>
`pt --host 192.168.1.10:8080 --username admin --password 'mypassword' import newusers.yml`
* If you encounter any error messages, check the server logs to identify the offending statement (put `com.egis.kernel.messaging` on DEBUG/TRACE if additional logging is required)
