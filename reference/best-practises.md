## Best Practises


### Testing Data

Test data (users, groups, permissions, etc) should be combined into a single `test/TestData.yml` i.e the `install` and `upgrade` folders should match the production environment. 

### Configuration

* For large and complex configurations break down YAML files into multiple logical sections, just ensure they are named with an appropriate prefixes if they are interdependant e.g. 
  * `Z0.DataSources.yml`
  * `Z1.ListIndex.yml`
  * `Z1.Node.root.yml` - Root folder structure with no indexes or rules
  * `Z2.Node.yml` - Node structure with indexes and rules
  * `Z3.Groups.yml` - Groups and roles - Test users should go into `TestData`
  * `Z2.Permissions.yml` - Global permissions and Node tree with permissions only (excluding rules and indexes)

### Node Structure and Taxonomy

* Index names should be: **lower_case**  
* Node names should be: **Human Readable** and *short  *
* User folders or a folder per user is an **anti-pattern**, User, Owner or Creator context permissions are often more suitable  
