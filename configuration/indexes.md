# Configuring Node Indexes / Fields

### Index Types

| Type            | Description                              | Example                              |
| --------------- | ---------------------------------------- | ------------------------------------ |
| Text            |                                          |                                      |
| Long Text       | A comment box that can accept many lines of text.  **Warning:** Builtin notes and comments are most likely a better option |                                      |
| Date            | A date in yyyy-mm-dd format              | 2011-12-31                           |
| Date Time       | A date with a time in yyyy-mm-dd hh:mm format | 2011-12-31 08:00                     |
| Number          |                                          | 1                                    |
| Double          |                                          | 1.15                                 |
| List            | Selectable list                          |                                      |
| Long List       | Autocomplete list - user needs to enter at least 1 letter |                                      |
| Auto Number     | Generated on create, non editable        | REF001                               |
| UUID            | Generated on create, not editable        | be8ca9db-1e8c-4c27-8aad-52f974109f64 |
| Document Picker |                                          | document.docx                        |
| User Picker     |                                          | John Doe                             |
| DB Lookup       | **Depreceated** Use a datasource backed list instead |                                      |



### Scripting - Front End

The `custom` property can be used to configure a field at runtime, it accepts valid javascript object 

e.g Create a `TEXT` field called ID Type and then add

```javascript 
{
	type: 'formcombo',
	types: {
		"ID": "ID Meta Model",
		"Passport":"Password Meta Model",
	},
	value: 'Payslip'
}
```

Then create a metamodel for each document type:

```yaml
--- !<MetaModel>
name: ID Meta Model
fields:
- ID No

--- !<MetaModel>
name: Passport Meta Model
fields:
- Passport No
- Country of Issue
- Expiry Date
```



When a user selects **ID** a `ID No` field will be shown which can include validation for length, etc. If they select **Passport** A `Passport No`, `Country of Issue` and `Expiry Date` fields will be shown

### Scripting - Server Side

**Default Value** is used when a document is created without an index value 

e.g. `${new Date():yyyy}` will automatically populate a year index with the current year.

See [Standard Expression](../reference/standard-expression-text.md)

**Regex** is a Java regular expression that is evaluated server side, if the value does not match the user is shown a validation error.

See [Regular Expressions](../reference/regex-text.md)

**Filter** are evaluated just before an index value is saved, it accepts any Groovy statement

e.g.

Remove whitespaces:

```Java
value.replaceAll("\\w*", "")
```

Strip out all non digits:

```java
value.replaceAll("\\D+", "")
```

Uppercase and trim:

```java
value.toUpperCase().trim()
```



### Properties

**Name** - The name used in the database - Index names cannot be changed after they are created. 

**Case Sensitivity** - All indexes with a common name need to be in the same case, PaperTrail will automatilly change the case if an indexing index in a different node has a different case.

> While indexes names are case sensitive, their use within queries, scripts and expressions is case *insensitive*

**Mandatory** vs **Required**  - Required indexes have a hard restriction server side, they can never be empty. Mandatory indexes are only restricted on a user interface level. e.g. Does not affect systematic imports via API, Folder Watch, Email Watch etc..

> If a required index is added to a node which already has documents, the index will need to be populated before anything else can be done with those documents)



**Read Only** Indexes can oinly be set on import, thereafter they are non editable

