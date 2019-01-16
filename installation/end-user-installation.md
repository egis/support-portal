## Installation and Configuration

## System Requirements
The minimum requirements that are advised for Workstations are as follows:

*  2-4 GB RAM  
*  Dual Core i3/i5 CPU  
*  Internet Explorer 11/Edge OR  
*  Chrome (latest stable release) OR  
*  Firefox (latest stable release)  

### Advanced Plugin
1. Click on Help / Cog -> Check Installation and then follow the instructions that will guide you through the installation process

See [Windows](desktop-agent.md)

For silent installation use following command:
```
PaperTrailSetup.exe /S
```

### Desktop Agent

Download and run the installer from [http://downloads.papertrail.co.za](https://downloads.papertrail.co.za/Desktop)

See [Windows](Desktop Agent) and [Linux](Ubuntu-Linux)
### Office Addin

Download and run the installer from [http://downloads.papertrail.co.za](https://downloads.papertrail.co.za/Desktop)

See [MS Office Add-in](MS Office Add-in)
### Web Scan

Web scan is distributed as an add-on to the Advanced Plugin:

1. Install the Advanced Plugin
2. Download and Install the Web Scan Add-on from [Downloads](https://downloads.papertrail.co.za/scan)
3. Configure scan profiles under System -> Scanning

### Wacom Signature Pad

To set up the Wacom Signature Pad on an end user's machine please follow below:

1. Download the latest drivers for the signature pad from [Wacom's website](https://www.wacom.com/en-in/support/product-support/drivers)
* Before installing the drivers ensure that the signature pad is not plugged in
* Run the Driver installer
* Once the installation is complete, restart the computer
2. Ensure the user has the PT advanced plug-in installed
3. Download the PT "BioSign" addon, found [here](http://s3.amazonaws.com/papertrail/public/plugin/PaperTrailAddonBioSignSetup.exe)
4. Go to the desired PT location from the user's browser
5. Plug the signature pad into the computer
6. Before logging in open the developer console
7. Log into PT, check the initialisation steps found in the console, if the "BioSign" addon was successfully installed it will be noted as initialised
8. To test that the signature pad works, `Upload for Signature`
9. Place a signature on the document and `Sign Now`
10. Upon clicking the `Signature` field a signature block will be displayed on Wacom tablet
