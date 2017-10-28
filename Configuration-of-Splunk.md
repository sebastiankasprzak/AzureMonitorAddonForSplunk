## Selecting your cloud
(version 1.2.3)
If you operate in a cloud other than Azure Public Cloud, you can select your cloud by editing BOTH of azure_activity_log.sh AND azure_diagnostic_logs.sh, which are located in TA-Azure_Monitor/bin. There are comments in the files that direct you on how to make the edits.

At this time, the available clouds are: Azure Public Cloud, Azure US Government, Azure China Cloud, Azure Germany Cloud.

## Data Input Settings
To create a new instance of one of the data inputs, in Splunk Web go to Settings / Data Inputs. Find the data input that you want in the list:
* Azure Monitor Activity Log
* Azure Monitor Diagnostic Logs
* Azure Monitor Metrics

Drill in and click the "Add New" button, or click "Add New" on the far right in the list.  

The parameters are:  

NOTE: The Metrics data input is the only one that uses subscriptionID. The Activity Logs and Diagnostic Logs are the only ones that use an event hub. The rest of the fields are shared by both. 

| Parameter Name | Value | Notes |
|----------------|-------|-------|
| name | string | I use the name of the monitoring target - in my case the name of my subscription |
| SPNTenantID | \<guid\> | the tenant id of your Azure AD tenant |
| SPNApplicationID | \<guid\> | the application id of your service principal |
| SPNApplicationKey | \<password\> | the secret key to the service principal |
| eventHubNamespace | string | the name of your Event Hub |
| subscriptionId | \<guid\> | your Azure subscription ID |
| vaultName | string | the name of your Key Vault |
| secretName | string | the name of the secret containing the "real work" credentials |
| secretVersion | string | the version number of the "real work" secret |

NOTE: When you create an Event Hub, you're really creating an Event Hub Namespace. Within that Event Hub Namespace a number of Event Hubs will be created as your resources emit logs. So, the term "Event Hub" is overloaded. The name of your Event Hub Namespace is the name you used when you created your "Event Hub". Confused?

Example of data input parameters form:  
[[images/SplunkDataInput.PNG]]

Here's what it looks like getting the key vault secret's version:  
[[images/keyVault3.PNG]]

And here's a sample of a filled in data input configuration panel:  
[[images/SplunkDataInput2.png]]

## JSON lookup files

### logCategories.json
Found in TA-Azure_Monitor/bin/app

This file contains a list of the log categories supported by Azure Monitor. Each one is paired with a sourcetype. Feel free to adjust the sourcetypes to your own needs. If you delete a line, the sourcetype will be the default sourcetype that you entered in the data input settings.

### hubs.json
Found in TA-Azure_Monitor/bin/app

This file contains a list of the event hubs used by diagnostic logs, which equates to a list of the log categories available for resources that emit diagnostic logs. This file should not be usually be editted. The value associated with each key is how the program looks up the resource id in messages coming from any particular hub. If you don't want a particular hub to be drained of messages and indexed in Splunk, remove the line from the file.

### sourcetypes.json
Found in TA-Azure_Monitor/bin

This file contains a list of resource types that emit diagnostic logs and the sourcetype for each. Add lines as needed if you want distinct sourcetypes for your Azure resource types. Or delete lines if you want to use the default you entered in data input settings. This has no impact on Activity Log; only the sourcetypes for Diagnostic Logs are impacted.
