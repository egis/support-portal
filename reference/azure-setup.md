# General 

## Prerequisites

OAuth authentication for EWS is only available in Exchange Online as part of Microsoft 365  
EWS applications that use OAuth must be registered with Azure Active Directory.  

## Required keys

* Application (client) ID - client_id
* Directory (tenant) ID - tenant_id
* Secret Value (Not Secret Id)
  * This disappears once it is created and window changes - secret_value 
  * <p style="color: red;font-weight: bold">NB: This is only for Application Access</p>

# Setup

Go to the [Azure Portal](https://portal.azure.com/#home)  
Click ‘view’ under “Manage Azure Active Directory” > “App registrations”  
Either Click to edit a Registered App or click on “New registration”
Under “Authentication” , Setup Supported Account Types and Advanced Settings  


## Authentication
### Setup Supported Account Types and Advanced Settings
### Enable “Allow public client flows”


### The following are Default URLs
```text
https://login.microsoftonline.com/common/oauth2/nativeclient
https://login.live.com/oauth20_desktop.srf
msal{client/tenant id}://auth
```

### Setup the following Custom Redirect Urls

```text
http://127.0.0.1/
urn:ietf:wg:oauth:2.0:oob
```

# Delegated Access

## API Permissions

Add the following DELEGATED permissions found under `Office 365 Exchange Online`

* EWS.AccessAsUser.All
* Mail.Read
* Mail.Read.All
* Mail.Read.Shared
* Mail.ReadBasic


Click the `Grant admin consent for *****`

It should show `Granted For ****` under the status column for the above rows 

### <div style="color: red">NB: Type column for the above should be `delegated`</div>


## Expose an API:

### Add the following scopes:

| Scope Name | Who Can Consent? | Admin consent display name | Admin consent description | User consent display name | User consent description | State   |
|------------|------------------|----------------------------|---------------------------|---------------------------|--------------------------|---------|
| Mail.send  | Admins and users | Send Mail                  | Send Mail                 | Send Mail                 | Send Mail                | Enabled |
| PTScope    | Admins and users | Read                       | Read                      |                           |                          | Enabled |


## Manifest

### Add the below object to the `requiredResourceAccess` array

```json

{
  "resourceAppId": "00000002-0000-0ff1-ce00-000000000000",
  "resourceAccess": [
    {
      "id": "3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5",
      "type": "Scope"
    }
  ]
}

```

## App Roles

### Add a new Role

| Display Name | Allowed Member Types               | Value                    | Description | Do you want to enable this app role? |
|--------------|------------------------------------|--------------------------|-------------|--------------------------------------|
| Impersonate  | Both (Users/Groups + Applications) | ApplicationImpersonation | Impersonate | True                                 |

# References

[Azure Portal](https://portal.azure.com/#home)
