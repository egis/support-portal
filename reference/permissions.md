| Permission                               | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| ADD_LINK, DELETE_LINK                    |                                          |
| ADD_NOTE                                 |                                          |
| ADD_REMINDER                             |                                          |
| ADD_ATTACHMENT, DELETE_ATTACHMENT, DELETE_OWN_ATTACHMENT | Consider ADD_LINK instead <br> DELETE_OWN is similar to DELETE CREATOR permissions on documents |
| BULK_DOWNLOAD                            | Still required underlying READ_CONTENT   |
| CHANGE_VISIBILITY                        |                                          |
| COPY, MOVE                               | IMPORT permission is still required on the to folder |
| DELETE                                   | Automatically creates an item in System/Trash |
| EXPORT                                   |                                          |
| EMAIL                                    | Email external parties or contacts a copy of the document as an attachment and therefore requires EXPORT |
| NOTIFY                                   | Emails internal users a link to the document |
| SHARE                                    | Emails external users a secure link to the document or folder |
| FILE                                     | Remove an item from your mydocs          |
| FORWARD                                  | Forward a document **already** in your mydocs |
| RETRIEVE                                 | Add a document your mydocs               |
| READ                                     | Access to view the document in the grid  |
| READ_ATTACHMENT                          |                                          |
| READ_HISTORY                             |                                          |
| READ_NOTE                                | Can apply on multuple visibility and owner levels. Notes cannot be updated or deleted |
| READ_CONTENT, WRITE_CONTENT              | Access to view and update the actual documents |
| READ_METADATA, WRITE_METADATA            | Can apply on index levels as well        |
| RESTORE_VERSION                          | Still required READ and WRITE content    |
| SIGN                                     | eSign a document                         |
| TAKE_OWNERSHIP, ASSIGN_OWNERSHIP         | Assign applies if their is no owner, takes applies if their is an existing owner |
| DIARIZE                                  | Use ADD_REMINDER instead                 |
| ROUTE_FORWARD, ROUTE_BREAKOUT            | Use simple workflow's instead            |
| RECALL, RECALL_OWN                       | Caution: The use of recall should be for exceptions, if it is used regularly then a queue probably more suitable |
| PRINT                                    | Legacy, don't use                        |



## Node Permissions

| Permission       | Description                              |
| ---------------- | ---------------------------------------- |
| SEE_PARENT_ONLY  | When folders are using to manage large volumes of documents, apply this permission so that only the parent node is visible and not all sub folders. Prevents navigating through folders and forces users to search |
| SEE              | See the node only, READ permissions still need to be applied to documents using CREATOR or OWNER context |
| READ             | See the documents in the node, (READ_* permissions still required to view the files, history, notes etc..) |
| IMPORT           | Import documents into a folder. Only makes sense in an ALL context |
| NODE_ADMIN       | Create folders and manage indexes and rules |
| FOLDER_ADMIN     | Create folders only                      |
| PERMISSION_ADMIN | Add permissions to a folder              |
| SHARE            | SHARE an entire folder with an external user via an external link |



## Misc Permissions

| Permission   | Description |
| ------------ | ----------- |
| VIEW_REPORT  |             |
| REQUEST_FORM |             |
| QUEUE_TAKE   |             |



## Admin Permissions

| Permission          | Description                              |
| ------------------- | ---------------------------------------- |
| ADMIN               | Access to Admin Dashboard                |
| BULK_ADMIN          | Bulk Move, Delete, etc                   |
| CONTACT_ADMIN       | Create, edit, remove contacts            |
| CUSTOM1,2,3         | Used for custom development purposes only |
| IMPORT_ADMIN        | Create, edit and remove email and file imports |
| LIST_ADMIN          | Create, edit and remove lists and list values |
| OUT_OF_OFFICE_ADMIN | Manage out of office settings on behalf of other users |
| RECORDS_MANAGER     | Manage the File Plan with the RM module installed |
| ROUTE_BREAKOUT      | Legacy                                   |
| PERMISSION_ADMIN    | Add new permissions                      |
| TEMPLATE_ADMIN      | Create, edit and delete document templates |
| WORKFLOW_ADMIN      | Create, edit, import and export workflows |
| USER_ADMIN          | Create, edit, and remove users. Reset passwords |
| USER_CREATE         | Create new users, but not update existing or reset passwors |

