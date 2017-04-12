## Data Input Settings
To create a new instance of one of the data inputs, in Splunk Web go to Settings / Data Inputs. Find the data input that you want in the list:
* Azure Monitor Activity Log
* Azure Monitor Diagnostic Logs
* Azure Monitor Metrics

Drill in and click the "Add New" button, or click "Add New" on the far right in the list.  

The parameters are:  

NOTE: the Logs use eventHub, whereas the Metrics use subscriptionId. The rest of the parameters are needed in both.

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

## JSON lookup files

### logCategories.json
Found in TA-Azure_Monitor/bin/app

This file contains a list of the log categories supported by Azure Monitor. Each one is paired with a sourcetype. Feel free to adjust the sourcetypes to your own needs. If you delete a line, the sourcetype will be the default sourcetype that you entered in the data input settings.

### hubs.json
Found in TA-Azure_Monitor/bin/app

This file contains a list of the event hubs, which equates to a list of the log categories. This file should not be editted. The value associated with each key is how the program looks up the resource id in messages coming from any particular hub.

### sourcetypes.json
Found in TA-Azure_Monitor/bin

This file contains a list of resource types and the sourcetype for each. Add lines as needed if you want distinct sourcetypes for your Azure resource types. Or delete lines if you want to use the default you entered in data input settings.
