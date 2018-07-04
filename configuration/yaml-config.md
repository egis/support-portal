# YAML Import and Export

In addition to the various CSV and XML based exports available, a generic export/import interface is available via:
[via?]
Imports can be imported multiple times without creating duplicates, this can be used for updating configuration.

## Examples

### To import one or more entities:

```javascript
POST: /dao/import/yml
```

### To export all instances of an entity: 

```javascript
/dao/export/yml/{Entity}
```

To export a specific entity:

```javascript
/dao/export/yml/{Entity}?id={name}
```

Where {Entity} is one of:  

*  User *All permissions and group memberships will be retained*
*  Node *All child nodes, indexes, permissions and rules will be retained*  
*  ListIndex - All values will be retained.  
*  DataSource  
*  RuleApplication  
*  QueueConfig
*  MetaModel
*  Form  
*  Template  
*  All entities will export something - but the output may or may not import back in.  

Using [httpie](https://github.com/jkbrzt/httpie):  

```javascript
http --auth admin:test POST "http://localhost:8080/dao/import/yml" "Accept:*" < ~/test.yml
```
