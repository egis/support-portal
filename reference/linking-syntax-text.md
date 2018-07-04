# PaperTrail Document Linking Syntax
 

## Retrieving a document by docId

`GET: /public/file/100/test.doc`{.sql}

e.x : http://host:8080/public/file/100/test.doc
  
## Retrieving a document by path

`GET: /public/file/Division/cabinet/test.doc/dummy.doc`{.sql}

e.x : http://host:8080/public/file/Division/cabinet/test.doc.

Note : A dummy filename must be appended to the path e.g. dummy.doc
  
## Retrieving an attachment

`GET: /public/file/100/test.doc?path=attachments/att01.doc`{.sql}

e.x : http://host:8080/public/file/Division/cabinet/test.doc?path=attachments/att01.doc
  

## Retrieving a PDF for a document

`GET: /public/file/100/test.pdf?path=pdf`{.sql}

e.x : http://host:8080/public/file/100/test.pdf?path=pdf
  

## Retrieving a version of a document

`GET: /public/file/100/test.doc?path=versions/0.2/source`{.sql}

e.x : http://host:8080/public/file/Division/cabinet/test.doc?path=versions/0.2/source
  

## Retrieving a document via a query

`GET: /public/file/invoiceNo=AB123/test.doc`{.sql}

e.x : http://host:8080/public/file/Division/cabinet/test.doc?path=versions/0.2/source
  
## Query Syntax


| Properties        | Description
| ------------- |-------------
| Division/Cabinet/\*   | Returns all documents directly under Division/Cabinet.
| Division/Cabinet?recursive=true   | Returns all document under Division/Cabinet including documents in sub nodes.
| Division/Cabinet/test.doc   | Returns the document where the filename is test.doc in Division/Cabinet.
| Division/Cabinet/filename=test.doc   | Equivalent to the above query Division/Cabinet/filename=\*.doc and Returns all documents that end in .doc
| Division/Cabinet Division/Cabinet/filename\*=test   | Returns all documents that begin with test in Division/Cabinet.
| Division/Cabinet/test.doc?index1=value1   | Returns the document where the filename is test.doc and index1=value1 in Division/Cabinet
| Division/Cabinet/index=value   | Returns all documents where index1=value1 in Division/Cabinet.
| Division/Cabinet/index1=value1 & index2=value2   | Returns all documents where index1=value1 and index2=value2 in Division/Cabinet.


Note : index1=value2 : Returns all documents where index1=value1 in all nodes and folders Equals. 

```javascript
Equals = Not Equals != Contains *=* Starts With *= Ends With =* Between <=> Bigger Than (Number) >= Smaller Than (Number) <= After (Date) >>= Before (Date) <<= Is Empty !=!
```

