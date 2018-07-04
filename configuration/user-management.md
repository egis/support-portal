# User Management

In PaperTrail, a user is an individual who has **permissions to log in to PaperTrail and perform various functions, such as reading and editing documents**. 

A contact is an external user who **does not have a PaperTrail login name and password, but who can be e-mailed documents and reports by other PaperTrail users**.

## Create a New User

*  Let’s start by creating a new user called Sally Smith. Sally will have a username of sallysmith.  
*  From within the **Administration interface**, select **User Management** and then User from the Navigation menu.  
*  On the Command Bar, select **Add**.  
*  Specify all of the relevant fields for the new user. The Login field is the username that the user will use to log in. This name must not be currently used by an existing User, Group, Role, or Contact.  
*  If you need to synchronize this user’s account with their Active Directory account, click the **Active Directory checkbox**. The value supplied in the Login field must match the user’s Active Directory login (excluding the domain name).  
*  Click **Add** to generate the new user account.  

## Reset a User’s Password

*  From within the **Administration interface**, select **User Management** and then **User** from the Navigation Menu.  
*  Select the user whose password you need to reset, and click **Reset Password**. The password will be set to a blank password, which the user must then reset on their next login.  

## Create an Internal Contact List

The following steps should be followed to create a contact who can receive e-mail notifications from other users.  

*  From within the __Administration interface__, select __User Management__ and then  __Contact__ from the Navigation Menu.  
*  Specify a name for the user in the __Name__ field. This is the only required field; all other fields are optional.   
*  When done specifying information for this user, select the __Add__ button.  

## External LDAP contact list

*  External LDAP contact lists can be queried in order to populate email addresses for **Actions → Email**.  
*  Configure **Active Directory / LDAP settings**.  

## Create a Group

*  From within the **Administration interface**, select **User Management** and then Group from the Navigation Menu.  
*  Select **Add** on the Command Bar.  
*  Specify a **name** for the new Group, such as Sales Team. This must be a **unique name**; it cannot be the name of another User, Group, Role, or Contact.  
*  Select **Add** in the dialog box. The new group will be created.  

## Assigning a user to a group

To grant the permissions assigned to this group to a user, we simply add the user to this group.

-  From within the **Administration interface**, select **User Management** and then **Group** from the Navigation Menu.  
-  Select the group you created in the previous step, and then select **Users** from the Command Bar.  
-  In the **Users dialog**, begin to enter the name of the user you wish to add to the group. While typing, an autocomplete list of names will appear. Select the desired user to add, and then select the **Add button**.  
-  Select the **OK button** on the **Users dialog**.  
