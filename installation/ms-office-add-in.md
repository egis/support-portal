#PaperTrail MS Office Add-In
 
In these steps, we will see how to install PaperTrail MS Office Add-In 

*  Ensure that **Dot NET version 4 (.NET Framework)** is installed before installing the PaperTrail Add-In.  
NOTE: A computer reboot will be required if Dot NET is installed for the first time.

*  **Close all Microsoft Office applications** e.g. Word, Outlook, Excel, etc.  

*  If a previous release of the PaperTrail Add-In has been installed on the machine, please **uninstall the older version** before installing a later release. (Check the **Add and Remove Programs**, or **Program and Features section** for installed programs.)  

*  If the PaperTrail Add-in was previously installed on the computer, **delete the PaperTrail Add-In folder** after the application has been uninstalled. Default install paths to follow:

**MS Windows 7&8:** `..\Users\{user login}\AppData\Roaming\`

**MS Windows XP:** `..\Documents and Settings\Users\{user login}\AppData\Roaming\`

## Configuration 

To configure the plugin, 

*  __Host__ : Insert the URL, up until the port detail, used to access PaperTrail within your network / domain. 

Example: __http://{servername}:8080__. Replace the {servername} portion with the name or IP of the PaperTrail server.  

*  __Username__ : Enter PaperTrail username.  

*  __Password__ : Enter PaperTrail password.  

*  Click __Sign In__.  

![config](../images/msoffice-config-1.png)

## Troubleshooting

> Note : If the Plug-in cannot connect/authenticate, check if the user can connect to PaperTrail using a web browser on the user’s machine. Confirm that the user can login to PaperTrail with the same account details being used during the Plug-in authentication section.

It is possible that the MS Office application can fail to load the PaperTrail Add-In due to different reasons. If the PaperTrail Add-In is not available, check whether the Add-In has been disabled by the MS Office application in use. To access the disabled Add-In section follow these steps:

__To enable Add-in in Outlook 2003:__

Click **Tools -> Other -> Advanced Options -> Add-ins -> Manage -> Select Disabled Add-ins** from the dropdown and tick **PaperTrail Add-in**.

__To enable Add-in in Outlook 2007:__

Click **Tools -> Trust center -> Add-ins -> Manage -> Select Disabled Add-ins** from the dropdown and tick **PaperTrail Add-in**.

__To enable Add-in in Outlook 2010:__

Click **File -> Options -> Add-Ins -> Manage -> Select Disabled Add-ins** from the dropdown and tick **PaperTrail Add-in**.
