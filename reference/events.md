## Document Events

> Note all events listed below need to be prefixed with *Document.* e.g. **Document.add_attachment**

| Event             | Headers                                  | Description | Value |
| ----------------- | ---------------------------------------- | ----------- | ----- |
| activate          | user,allocatedBy,allocationId            |             |       |
| add_role          | parties,role                             |             |       |
| add_permission    | parties,permission                       |             |       |
| add_attachment    | filename                                 |             |       |
| add_note          | noteId, note, noteCreatedBy,noteCreatedDat, noteOwner |             |       |
| allocate          | isOutOfOffice,user,allocatedBy,allocationId |             |       |
| archive           |                                          |             |       |
| assign_owner      | owner                                    |             |       |
| audit             | auditTypeId,auditId                      |             |       |
| change_visibility | visibility                               |             |       |
| checkin           | version,currentVersion,comment           |             |       |
| checkout          | lockOwner                                |             |       |
| create            |                                          |             |       |
| copy              |                                          |             |       |
| delete            | bulk, source_docid                       |             |       |
| delete_attachment | filename                                 |             |       |
| diarize           | user,date,comment                        |             |       |
| filled            |                                          |             |       |
| link              | linkTypeId, from OR to                   |             |       |
| new               | from                                     |             |       |
| open              |                                          |             |       |
| restore           | oldVersion,version                       |             |       |
| read              | allocationId,user                        |             |       |
| recall            | user,allocationId                        |             |       |
| response          | from                                     |             |       |
| sign              | complete, reason                         |             |       |
| signCallback      |                                          |             |       |
| take              | queue                                    |             |       |
| trigger           | fired via /document/trigger/{id}         |             |       |
| unallocate        | allocationId                             |             |       |
| unassign_owner    |                                          |             |       |
| unlink            | from                                     |             |       |
| update            |                                          |             |       |
| update_content    | content                                  |             |       |
| update_index      | indexes                                  |             |       |
| update_json       |                                          |             |       |
| update_pdf        | complete, reason                         |             |       |
| view              | ip,path                                  |             |       |
|                   |                                          |             |       |

| Event                  | Headers | Description |      |
| ---------------------- | ------- | ----------- | ---- |
| Login.success          |         |             |      |
| User.logout            |         |             |      |
| User.activate          |         |             |      |
| User.deactivate        |         |             |      |
| User.resetPassword     |         |             |      |
| User.outOfOffice       |         |             |      |
| User.outOfOfficeReturn |         |             |      |
| **Entity**.insert      |         |             |      |
| **Entity**.update      |         |             |      |
| **Entity**.remove      |         |             |      |
| Property.update        |         |             |      |
| Session.create         |         |             |      |
| Session.destroy        |         |             |      |
| Cluster.start          |         |             |      |

