# Email Watch

## Import emails from a specific email account
1.  Add a new **Import Management -> Email Account**.  
1.  Add a new **Import Management -> Email Import**.  
1.  **Name** – Specify the name of the import - this will be recorded under the history tab.  
1.  Select the **Node** to import the document into.  
1.  Select the **Account** created in step 1.  
1.  Select an **Attachment** Policy  
		*  _Body Only_ - Import the .html or .txt email body only.  
		*  _Attachments Only_ – Import attachments only e.g .pdf, .word.  
		*  _Source Only_ - Import the email as a .eml suitable for search an preview.  
		*  _Document Archive_ – Used in conjunction with the autoExport rule.  
		*  _Threads_ – Update the original email with any replies – The Document.response event can be used to trigger notifications / workflows etc.
1.  Click Add.


## Filter spam or unwanted messages out
1.  Create one or more **Email Imports** with a Rule Order of 1.  
2.  Specify unwanted terms under the **Field** Tab e.g.  
3.  Create all other **Email Imports** with a Rule Order larger than 1.  

## Import emails from one email account with multiple aliases

1.  Create one **email account**.  
2.  Create one or more email import and specify the alias under the **Rules -> To** and **Rules -> CC** fields.  
3.  Select the **email account** created under step 1.  

## Map email fields to document indexes

1.  Select the **node to import the emails to**.
2.  Map the **fields** under the **Fields** tab.

## Exclude signature images and other attachments from being imported.

1.  Under the **rules** tab, specify a semi-colon separated list of **unwanted extensions** under Attachment Exclusion Filter.
e.g. *.gif;*.jpeg;*.png


OR


2.  Specify only the attachments you want to import under **Attachment Inclusion Filter**.
*.pdf;*.doc*

Update the original email when a reply is received (threading)

## Troubleshooting email imports:

1.  Ensure that standard email clients can connect over the POP and IMAP Protocols.
2.  Check **Services -> Properties -> Imports -> Debug POP/IMAP** to record the conversion with the POP/IMAP server to if it returns any error messages.
