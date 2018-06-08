# Advanced Permissions

Once you’ve added a user, you need to specify what features that user can access. PaperTrail offers an extensible permissions system that makes it easy both to assign basic permissions to a large number of users.

PaperTrail simplifies assigning permissions to users through two constructs: groups and roles. A group is a collection of users, while a role is a collection of permissions.


> Note: While it is possible to assign permissions to individual users, we recommend as a rule that administrators assign permissions to groups and roles, and then associate these groups and roles with users, as maintaining individual permissions becomes more complex as one’s user base increases.

When defining a permission for a group, role, or user, an administrator can specify one of three dispositions for that permission:  
-  **Permit** : Grants the permission to the specified entity.  
-  **Deny**: Forbids the specified entity from performing the defined action.  
-  **Important**: overrides a Deny permissions.  

## Permissions Context

Here is an overview of the different contexts in which permissions apply

| Permissions | Context 
| --------- | -------  
| All | Always Applies 
| Creator | Applies to the user who created a document. Note: In order to import a document in a node `Permission=Import Context=All` is required even though the Creator permissions will apply after import.
| Owner | Applies to the user or group currently set as owner of the document.
| User | Applies to all the currently allocated users.
| Past User | Applies to all previous users of a document.
| Record | Applies only to documents that have been declared a record.

Note: In order to a see a folder in the node tree, `Permission=SEE Context=ALL` permissions are required as only the All context applies to nodes

# Permission Assignment

## Role Creation

A set of permissions can be assigned to a role, and that role is assigned to one or more users.  

Roles should be used when permissions need to be doled out to individuals not based on their membership in a particular group or team, but based on their responsibilities within a company. 

1.  From within the **Administration interface**, select **User Management** and then **Role** from the **Navigation Menu**.  
2.  Select **Add** from the **Command Bar**.  
3.  On the **Add Role** dialog, enter a unique name for the **role** in the **Name** field. This name cannot be the same name as an existing **user, group, route, or role**.   
4.  Select the **permissions** to assign to this role from the available listbox, and then select the right arrow to add these permissions to the selected listbox.  
5.  Select **Add** to add the new **role** to the system.  


## Document visibility level

To create a new document visibility level :  


1.  Under **General → Visibility**  
2.  Click **Add**.  
3.  **Level**: Enter a unique numeric value e.g. 4.  
4.  **Description**: Enter a **description** for the visibility level e.g. Very High.  


## Global Permissions

To apply Global Permissions, follow the below steps :  

1.  Under **User Management -> Global Permissions** – Add any permissions required.
2.  Creating administrator level permissions.
3.  Global Administrators are defined as users with Admin on the Global Level.
4.  Administrators are anyone with an Admin permission.

## Administrator Permissions

To apply Administrator Permissions, follow the below steps :  

1.  Global Administrators are defined as users with Admin on the Global Level.  
2.  Administrators are anyone with an Admin permission.  

## Denying Permissions to User

Denying users out of a group permissions on a node :  

1.  Give the **group permissions** on the node with `Type = Permit`.  
2.  Deny the **user permissions** by using `Type = Deny`.  

## Creator's permissions

1.  Apply **permissions** in the **CREATOR** context

## Owner's permissions

1.  Apply **permissions** in the **OWNER**  context

## User's / Collaborator's  permissions

1.  Apply **permissions** in the **USER**  context 

## Restrict Specific Node access 

To deny administrators access to specific node, follow the below steps :  

1.  Give a user (e.g. HR Manager) **IMPORTANT Permission Admin** on the node 
> IMPORTANT: This step must be completed first and verified or there is risk of being locked out of the node
2.  Apply **DENY Permission Admin** to Everyone.  
3.  Once applied only the user specified in step 1 will be able to add or remove permissions.  
4.  Apply any other **DENY permission** required e.g. (Deny Role All to Everyone)  
5.  Apply **IMPORTANT permissions** to give  access e.g. (IMPORTANT READ to HR Group)  

## Applying Index Level Permissions

Permissions in PaperTrail are highly granular, and can even be applied to individual indexes.

1.  Within the **Nodes interface**, select a node.   
2.  In the **Object Browser**, select an existing index for that node  
3.  From the **Command Bar** on top of the Object Browser, select **Permissions**.  
4.  Only two permissions can be set on a node, **Read Metadata** and **Write Metadata**.  
5.  Select one of these permissions from the **Permission drop-down**.  
6.  Select whether this permission to either **Permit, Deny, or Important**.  
7.  Specify the **User or Group** to whom this permission applies. As you type a value in this box, PaperTrail will display an auto-completion list of matching users and groups.  
8.  Select the **Add button** to add the **specified permission** to the index.  
9.  Repeat this process to add as many permissions to this index as needed. When you are done adding permissions, select the **Close** button.  

## Site-Wide Administrator

> WARNING: This permission grant gives a user “superuser” access to your PaperTrail installation; it should only be granted rarely, and only to trusted individuals within your organization. Before granting site-wide administrator permissions, consider granting a more limited set of permissions for a specific purpose, such as 
List Admin or Node Admin.

To make another user a site-wide administrator, an existing administrator can grant an existing user the ALL role.   


1.  From within the **Administration interface**, select **User Management** and then **Global Permissions** from the Navigation Menu.  
2.  Click **Add** on the Command Bar.  
3.  Leave the **Permission** field blank.  
4.  From the **Role drop-down**, select All.  
5.  Leaving all other fields as is, select the **Add button**. The specified user will now have access to all administrative features of the site.  

## License Type 

To change the license,

1.  Update **Services -> Properties -> General ->License Code**. 

## V2 Portal - not able to see root level nodes

With the V2 Portal interface, user cannot see the child node(s) that they have access to, unless See permission is granted on the top level node as well. See JIRA PPT-11403.
To resolve this, add `ui.full.tree.query=true` to the properties file (V8.8.8 b1354 onwards)


