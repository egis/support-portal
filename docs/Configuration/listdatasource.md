# Pulling List values from a Node Data Source

Before proceeding, please see Jira issue OFF-484 (Can't use office plugin with a data source list)

### 1. Setup a system node to house the list data
* Settings > Administration > Node Management<br>
* Create a child node under `System` (e.g. System/configs/codes)
* Assign Permissions:
  - Role: ALL, User: Administrator, Type: Important
  - Permission: Read, Group: Everyone, Type: Permit
  - Permission: See, Group: Everyone, Type: Deny<br>
* Add Indexes:
  - Code
  - Name
  - filename

### 2.1 CSV file to import items into node (optional, alternately choose step 2.2)
* Set up a CSV with fields
  - Code
  - Name
  - filename
* Where:
  - Code = Value
  - Name = Description
  - filename = f_Code_Name [Excel statement: `=CONCATENATE("f_",A2,"_",B2)`]
* Import this CSV file into the node created in step 1:
  - Settings > Administration > Services > Tasks > Bulk Import > Bulk Import (.csv) > Import
  - Select the CSV file and the `System/configs/codes` node to import to

### 2.2 Manually create the values in the node (alternate to step 2.1)
* From the front-end UI, Document > Create and populate the Code, Name and Filename indexes
* Repeat for each list value you want to create

### 3. Add a Data Source referencing the Node
* Settings > Administration > Services > Data Source > Add
* Set a Name
* Set the Type to LOCAL_DB
* Write the Query:
  - `select Code as value, Name as description from dbo.document_summary_index where nodeId = '100'`
* Replace `nodeId = '100'` with the actual nodeId of the node your created in step 1
* PQL option: `SELECT Code, Name FROM System/configs/codes LIMIT 500`

### 4. Reference this node as the data source for your list
* Settings > Administration > Services > List Management > List
* Create / Edit the list
* Select the Data Source from point 3 in the Data Source dropdown
