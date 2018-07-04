# Papertrail Linux CLI command: pt

A command line interface to perform functions not found in the administrative GUI is available. It can also be used as part of a scripting process, e.g. bulk export/upload etc. This utility can be installed on Linux via pip (package management system to install Python software packages).

### Requirements:
It is not necessary for this program to be installed on the Papertrail server that you intend on connecting to. However, the following packages need to be installed on the Linux host where you intend on using the `pt` CLI command:
 * Python
 * pip
 * Git
 
The installation of these packages may vary depending on the flavour of Linux running (e.g. *yum*, *rpm*, *apt-get*)

### Installation
* `sudo pip install papertrail-cli`

### Usage
 * Once installed, executing `pt --help` will bring up the available options and commands. Use `pt {command} --help` for more details on the specific command itself; e.g. `pt import --help`
 * To connect to a Papertrail host server:<br>
    `pt --host 192.168.1.10:8080 --username admin --password 'mypassword'` (which will not execute an actual command; enclose password in single quotes if it contains special characters)
 * Add onto the above for the specific function you wish to achieve, e.g.<br>
    `pt --host 192.168.1.10:8080 --username admin --password 'mypassword' export User > users.yml`
 * Another example:<br>
    `pt --host 192.168.1.10:8080 --username admin --password 'mypassword' import newusers.yml`

### Reference
 * The above 2 examples export and import users respectively based on the YAML format. See more [here](../configuration/yaml-config.md)
 * Further details specific to the user import and export process can be found [here](../configuration/user-export-and-import.md)
