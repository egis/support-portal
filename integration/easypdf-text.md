# EasyPDF deployment and configuration

## Software Requirements

The following software will have to be installed on the EasyPDF server :   
1.  Windows Server 2008 32/64 bit.  
2.  PaperTrail 32 bit (latest release available).  
3.  EasyPDF version 6/7 32 bit.  
4.  EasyPDF PaperTrail Addon 32 bit (EasyPDF 6 requires Addon r5453
and EasyPDF 7 requires Addon r8738).  
5.  Microsoft Office 2010.  
6.  Any other native applications that may need to be converted to
PDF by EasyPDF (i.e. AutoCAD).  

**Note : UAC should be disabled on the machine before any software is
installed.**

## Local Installation
(Both PaperTrail and EasyPDF running on same host) :

*  Install EasyPDF application.
*  Install PaperTrail release.
*  Install EasyPDF PaperTrail Addon.
*  Set the “BCL easyPDF SDK 7 Loader” and “Papertrail” services to
run as the same account which should be granted administrative
permissions.
*  Start PaperTrail and confirm that installation was successful.
*  Add the following line to the easypdf.properties file and restart
PaperTrail thereafter :

```javascript
easypdf.word.nativeOfficePDF=true
```

* Import test documents to confirm that all is set up correctly.

## Remote Installation 
(Both PaperTrail and EasyPDF running on separate hosts) :

**EasyPDF server**

Same as [Local Installation](#local-installation)

 **PaperTrail application server** :

1. Once PaperTrail is up and running, set the below properties in
the papertrail.properties file to enable remote conversions :
```html
conversion.filetype.\*=remote
conversion.filetype.pdf=pdf
conversion.remote.host=http://host1:8080
```
2. Import test documents on application server to confirm that all
is set up correctly.

## Troubleshooting

If any conversion issue are being experienced, create a .vbs
file which can be run to test conversions outside of PaperTrail. The
paths in the properties are input and output files, and should be
configured accordingly:

```javascript
Set oPrinter = CreateObject("easyPDF.Printer.7")
Set oPrintJob = oPrinter.PrintJob
oPrintJob.PrintOut "C:\\test.txt", "C:\\output.pdf"
```
 

Another way to test the conversions is to navigate to
`C:\\Users\\Public\\Documents\\BCL Technologies\\easyPDF SDK
7\\Samples\\Visual C\#\\EasyPDFPrinterTest` and then running
`EasyPDFPrinterTest.exe`. This will allow you to select an input document
to convert and specify the output path of the PDF.

 

For any more information, the user manual can be accessed [here](http://www.pdfonline.com/easypdf/sdk/usermanual/)
