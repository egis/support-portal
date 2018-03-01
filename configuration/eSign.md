# eSign

### Requirements and Preparation
* Ensure that the client is licensed for the eSign module
* Administration > Services > Properties > Front End:
  * Ensure that `pdf_sign`, `upload_for_signature` are not listed under Disabled Actions
  * If anything is changed here, a restart of the PaperTrail service is required
* Administration > Services > Properties > eSign:
  * Set the `eSignature Upload Node` (ensure that users that will be designing templates have sufficient permissions here)

### Creating a Design and a Template
* V2 Interface: Select `eSign`. Click `Upload for Signature` and select the source document
* Classic Interface: Select `Tools > Upload for Signature`
* In the new tab (ensure that pop-ups are not blocked), set fields etc and then add the Signature box(es)
* Signatures can be open to anyone (leave the `Name` field blank), or restricted to a specific user via the `Name` field
* When done, click the disk (Save) icon to save the design. This saves the form design under the `eSignature Upload Node` defined in the Requirements and Preparation stage.
* Then click the Settings cog and `Save as template`. Name the template and select the node that this template will reside in. This is the location where the created forms will save to

### Signing Documents
* V2 Interface: Navigate to `eSign` and select the form > `New Request`
* Classic Interface: `Tools > New Form`
* Signed documents will be created in the node specified under `Save as template`

### Notes
* To edit an existing design, V2 Interface: select the design by clicking `eSign` and selecting the design you wish to edit. Then `More > Sign`. Save the design and the template
* To edit an existing design, Classic Interface: select the design from the `eSignature Upload Node`. Then `Document > Sign`. Save the design and the template
* To auto-populate indexes based on values in the form, name the `Field ID` in the design stage to the same as the index you wish to populate.
