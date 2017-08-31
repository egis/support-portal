# System Nodes

The `System` node has a number of nodes that have special behaviours:

### System/images

PaperTrail logo's are located here and can be updated with custom image's if required.  

* Images must end in .png (if they are a .jpeg or .gif they can be safely renamed).
* Images should be the correct size, if the image is bigger or smaller it should be manually resized before importing into System/images.
* To prevent the images from being overwritten after upgrades, they should be permanently checked out.
* All images should be transparent


`papertrail.png` (110x26)  
The logo that sits in the top left of the classic app  

`logo_big2.png` (250x68)  
The logo on the login page and portal app  

`logo_big2_white.png` (250x68)  
A white logo for dark themes in portalapp  

> Note the contents of this folder are publicly accessible and should not be used to store sensitive images

### System/templates

Contains all the base document templates and also the email templates used for notification bodies:

Email templates can used layouts by appending the layout name to the filename e.g. `account-signup_notitication.html` will use the the `System/templates/layouts/notification.html` layout to create pretty HTML emails.

### System/scripts

Contains groovy files that are run on startup - Often used for creating services

### System/jars

Contains precompiled JAR files that are loaded at runtime, functionally equivalent tot he local `deploy` filesystem directory but offers simplified management especially due to backup/restores and solution deployment

### System/plugins

Any `.js` file within subdirectories will be loaded into the browser to allow customization of the UI. Supported folders are:

* webapps
* admin
* eSign
* AdminApp
* PortalApp
* BulkCapture

e.g. `System/plugins/PortalApp/plugins.js` will be loaded for the modern portal UI

