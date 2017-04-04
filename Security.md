## Overview
Azure Monitor Logs (Activity and Diagnostic) are delivered via Event Hubs. An event hub is accessed using a policy name and key. These values are stored in a Key Vault secret. The Key Vault credentials necessary to retrieve the secret from the key vault are part of the configuration of the data input. A complete set of credentials in this case are Key Vault credentials + Event Hub credentials.

Azure Monitor Metrics are delivered via REST API. The REST API is accessed using a service principal name and password. These values are stored in a Key Vault secret. The Key Vault credentials necessary to retrieve the secret from the key vault are part of the configuration of the add-on. A complete set of credentials in this case are Key Vault credentials + REST API credentials.

The Azure Security Admin persona owns the Event Hub credentials and the REST API credentials that do the "real work" (and are stored as secrets in Key Vault) as well as the Key Vault credentials that can access the secrets. He shares the credentials that can access the secrets (as part of the configuration of the add-on) with the Splunk Admin persona, but not the credentials that do the "real work".

There is one complete set of credentials for each instance of data input. 

## Security Overview
[[images/security1.PNG]]