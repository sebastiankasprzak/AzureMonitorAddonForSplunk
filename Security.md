## Overview
Azure Monitor Logs (Activity and Diagnostic) are delivered via Event Hubs. An event hub is accessed using a policy name and key. These values are stored in a Key Vault secret. The Key Vault credentials necessary to retrieve the secret from the key vault are part of the configuration of the data input. A complete set of credentials in this case are Key Vault credentials + Event Hub credentials.

Azure Monitor Metrics are delivered via REST API. The REST API is accessed using a service principal name and password. These values are stored in a Key Vault secret. The Key Vault credentials necessary to retrieve the secret from the key vault are part of the configuration of the add-on. A complete set of credentials in this case are Key Vault credentials + REST API credentials.

The Azure Security Admin persona owns the Event Hub credentials and the REST API credentials that do the "real work" (and are stored as secrets in Key Vault) as well as the Key Vault credentials that can access the secrets. He shares the credentials that can access the secrets (as part of the configuration of the add-on) with the Splunk Admin persona, but not the credentials that do the "real work".

There is one complete set of credentials for each instance of data input. 

## Security Overview
[[images/security1.PNG]]

## Service Principals

### Key Vault credentials

All data inputs need this one. You could use only one of these across all of your data input instances, or as many as make sense in your security scheme. This step is performed by the Azure Security Admin persona.

#### Create the Service Principal application and get the application ID & Key

* Follow the steps in this documentation page to create your Service Principal application and key: [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal#create-an-active-directory-application).
* Do the next step on the page: Get the Tenant ID. Save it aside for the moment.

#### Configure Application

* Do the next step on the page: Assign application to role. 
* Navigate to your Key Vault in the portal.
* Assign your application to the Reader role on the Key Vault according to the steps in the document.
* Give your application permission to GET secrets from your Key Vault, as depicted:

[[images/keyVault1.PNG]]

### REST API credentials

The metrics data input requires this one. You may use the same Service Principal application for this that you did for Key Vault credentials, or you can create a separate one. This step is performed by the Azure Security Admin persona.

If you're going to create a separate Service Principal for this one, use the same instructions as above.

Either way, you must:

#### Configure Application

* Do the next step on the page: Assign application to role. 
* In this case the scope is your subscription.
* Assign your application to the Reader role on the subscription according to the steps in the document.

These values will be stored in your Key Vault.

## Event Hub

Get the policy name and key from your event hub. When your event hub was created, a policy named 'RootManageSharedAccessKey' was created by default and has the necessary permissions. As shown here:
[[images/eventHub1.PNG]]
Click through the list item to the next blade and copy the key as depicted here:
[[images/eventHub2.PNG]]
These values will be stored in your Key Vault.