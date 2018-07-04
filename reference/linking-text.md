## Manipulating the linking critera

### Linking Documents On Numbers Only

Specific node links can be added to only search the digit portion of the index value using IF ELSE logic, i.e.
```javascript
<Destination Node>/recursive=true&<Destination Index>=${if (<Source Index> == null) "" else <Source Index>.find("\\d+")}
```

where 

*  Destination Node: `<Root node/child node/>`
*  recursive=true: when searching over multiple child nodes
*  Destination Index: Index field you want to link to
*  Source Index: Index field on node you're linking from
*  ${if (<Source Index> == null): If source index has no Value
*  "" else <Source Index>.find("\\d+")}: Find matching Numeric Value


### Linking on Numeric with custom field Order_No
eg. Order_No = 12345

`<Destination Node>/recursive=true&Order_No=${if (Order_No == null) "" else Order_No.find("\\d+")}`

### Linking on Alphanumeric with custom field Order_No
eg. Order_No = PO12345

`"" else Order_No.find("\\w+")`
### Linking on Alphanumeric, Space, Numeric with custom field Order_No
eg. Order_No = PO 12345

     
### Regex Examples eg.
1)  **\\w+**    : All alphanumeric values

2)  **\\W**     : A non-word character: `[^\w]`

3)  **\\d+**    : All numeric values

4)  **\\D**     : A non-digit: `[^0-9]`

5)  **\\s**     : A whitespace character

