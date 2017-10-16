# Document Properties


Document properties are available to use in:

*   Node rule filters
*   Workflow filters
*   Standard Expressions e.g. the body field in a sendEmail rule

| Property       | Type          | Description                              |
| -------------- | ------------- | ---------------------------------------- |
| docId          | String        | The document unique identifier. Formatted as a PaperTrail document ID. e.g. `10034` |
| createdDate    | DateTime      | The date and time that the document was created. |
| lastModified   | DateTime      | The date and time that the document was last modified. Can be empty. |
| createdBy      | String        | The name of the user who created the document. |
| owner          | String        | The current owner e.g. `John`            |
| users          | CSV of names  | A list of currently allocated users e.g. `john, jane` |
| pastUsers      | CSV of names  | A list of users who were previously allocated the document e.g. `tom` |
| filename       | String        | The filename of the document including the extension. e.g. `test.pdf` |
| ext            | String        | A document extension suffix supported by PaperTrail. Does not contain the leading dot. e.g. `pdf` |
| name           | String        | The filename of the document excluding the extension e.g. `test` |
| node           | String        | The full path of the containing node e.g. `Division/Cabinet/Folder` |
| status         | String        | The status of the document.e.g.  `Filed`, `Current`, `Diarized`, and `Out` |
| size           | Long          | The size in bytes. Use this for a numeric comparison, for example: `size > 100000` |
| sizeFormatted  | String        | e.g.  `1 KB`, `5 MB`, `1 GB`             |
| visibility     | String        | .e.g. `Public`, `Private` and `Confidential` |
| editLink       | URL           | A link to either view the document or in the case of forms edit oonline |
| permLink       | URL           | A link to view the document              |
| title          | String        |                                          |
| subject        | String        |                                          |
| version        | String        | A document version number, e.g.  `2.1`. Can be empty. |
| _full_text     | String        | **Slow**: The full text contents of a document |
| _page_count    | Integer       | **Slow**: Returns the number of pages in a PDF document or an empty string |
| _httpIndexes   | String        | An HTTP URL encoded string of all indexes |
| _httpNodePath  |               | An HTTP URL encoded string of just the *node* path |
| _httpFilename  |               | An HTTP URL encoded string of *filename* |
| _model         | DocumentModel | **Advanced:** Returns the live object suitable for complex operations, cannot be printed directly |
| {custom index} | String        | Any custom index that is added under Node Management > Node > Index. |



### Writable Properties

Some document properties are also editable:

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

### Session Properties

| Document Property | Groovy Description | Description                              |
| ----------------- | ------------------ | ---------------------------------------- |
| dispatchedBy      | String             | For asynchronous rules, the user whose action triggered the event. Refer also to sessionUser. |
| sessionUser       | String             | For synchronous rules, the current user. For asynchronous rules, System. Refer also to dispatchedBy. |
| ip                | String             | The IP address of the user who performed the action that triggered the event. |
| now               | String             | ISO formatted timestamp                  |
| baseUrl           | URL                | The base URL that the server is accessible from e.g. `http://host:8080` |

## Special properties

Due to the large number of places, indexes/properties can be updated. It being the single most common point of integration between systems, there are a few special properties that trigger actions. They are prefixed with `_` and not to be confused with normal properties that relate to metadata only.  

| Document Property | Groovy Description                       |
| ----------------- | ---------------------------------------- |
| _audit            | Creates a new audit history event on the document |
| _status           | _status=Filed will remove all current users of a document _status=Archive will archive the document |
| _event            | Dispatches a new Document event          |
| user              | Allocates an user to the document        |
| owner             | Assigns ownership to the user            |
| node              | Moves the document to the specified node |
| visibility        | Changes the visibility of the document   |