# Document Export

## Command Line Process

Execute a command line process on a document. To do this, separate the command (script) and the file with: ||.   

If the path is not specified in the PATH environment variable, then specify the path. 
Examples:  

```javascript
autoPrint.vbs||${file}
C:\autoPrint.vbs||${file}
```

## Node Replication 

HTTP Path: The path to the PaperTrail server that will contain the replicated node.  

By default, a server can replicate to any other server. To prevent this behavior, refer to Trusted Servers, page.  

To see information about replication, to replicate documents again, and to clear replication queues, use the Rule.replicate message queue in **Services>Messages**.  

## Auto Export 

The autoExport rule can export documents via 3 different mechanisms:

### Folder

Folder supports multiple folder types:

| Syntax        | Description 
| ------------- |------------- 
| /folder/path    	    | Linux Format
| C:\\folder\path    | 	Windows Format
| \\server1\path   | 	Windows Only UNC style path - Note: Mapped drives are not supported
| smb://server1/path    | 	SMB/CIFS format supported on both Linux and Windows - Integrated Authentication is not supported
| ftp://server1/path     | 	FTP server supported on both Windows + Linux


### Email

Uploads the document via HTTP post to the specified host. If the URL does not contain a path then the following default is used:  

`/public/file/${_httpNodePath}/${_httpFilename}`

-  **${_httpFilename}** corresponds to  the URL encoded filename of the document  
-   **${_httpNodePath}** corresponds to the URL encoded node path  

This corresponds to the public API available for importing documents into PaperTrail.

-  To specify a different node path you would use:
`/public/file/Division/Cabinet/${_httpFilename}`  
-  To append indexes you would use:
`/public/file/${_httpNodePath}/${_httpFilename}?index1=staticValue1&index2=${docId}`  
-  And to append all indexes:
`/public/file/${_httpNodePath}/${_httpFilename}?${_httpIndexes}`  

### PaperTrail Server 


*  HTTP Path: The URL of the PaperTrail server to which the documents will be exported. Example: http://headoffice:8080  
*  Include: We recommend Document Archive or Source.  


## Export Format

*  Source - The original document  
*  PDF - The PDF rendition or the original document  
*  PDF Printout  - A PDF rendition that simulates a print to PDF event  
*  Document Archive - A ZIP file including all metadata and files  
*  XML - An XML file including all metadata  
*  Scripted - Allows the use of script to create FileObject from the a DocumentModel
 
