# Document Properties


Document properties are available to use in:

*   Node rule filters
*   Workflow filters
*   Standard Expressions e.g. the body field in a sendEmail rule

| Document Property        | Groovy Description           | Description  
| ------------- |-------------| -----
| docId   | String | The document unique identifier. Formatted as a PaperTrail document ID.
| createdDate   | Date | The date that the document was created.
| filename   | String | The filename of the document including the extension.
| lastModified   | Date | The date that the document was last modified. Can be empty.
| createdBy   | String | The name of the user who created the document.
| dispatchedBy   | String | For asynchronous rules, the user whose action triggered the event. Refer also to sessionUser.
| ext   | String | 	A document extension suffix supported by PaperTrail. Does not contain the leading dot.
| ip   | String | The IP address of the user who performed the action that triggered the event.
| name   | String | The filename of the document excluding the extension.
| size   | Long | The size in bytes. Use this for a numeric comparison, for example: size > 100000.
| sessionUser   | String | For synchronous rules, the current user. For asynchronous rules, System. Refer also to dispatchedBy.
| status   | String | The status of the document. Possible values are Filed, Current, Diarized, and Out.
| sizeFormatted   | String | Formatted as bytes. For example, 1 KB, 5 MB, 1 GB￼instead of an integer such as 14328490234..
| visibility   | String | Sets who is permitted to see the document. Valid values are Public, Private and Confidential..
| title   | String | Title.
| subject   | String | Subject.
| version   | String | A document version number, for example, 2.1. Can be empty.
| ???   | String | An index that is added under Node Management > Node > Index.


## Writable Properties

Some document properties are also editable, but most are read only.

*   filename
*   visibility
*   title
*   subject
*   {custom_index}

to set a writeable property you can use a script:  

`doc.metadata().set("title", "a new title")`

Or a updateIndex rule  

`title=new title`  

or using the HTTP API:  

`curl -x POST http://host/public/indexes/<docId>/?title= a new title`  

Document properties can also be updated via other mechanism for updating indexes including:

*   Import and Sync
*   .TXT files
*   .XML indexes

## Special properties

Due to the large number of places, indexes/properties can be updated. It being the single most common point of integration between systems, there are a few special properties that trigger actions. They are prefixed with `_` and not to be confused with normal properties that relate to metadata only.  

| Document Property        | Groovy Description  
| ------------- |-------------
| _audit	   | Creates a new audit history event on the document  
| _status	   | _status=Filed will remove all current users of a document _status=Archive will archive the document  
| _event	   | Dispatches a new Document event  
| user	   | Allocates an user to the document  
| owner	   | Assigns ownership to the user  
| node	   | Moves the document to the specified node  
| visibility	   | Changes the visibility of the document  
