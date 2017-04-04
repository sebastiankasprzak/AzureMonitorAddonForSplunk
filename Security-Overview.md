Azure Monitor Logs (Activity and Diagnostic) are delivered via Event Hubs. An event hub is accessed using a policy name and key. These values are stored in a Key Vault secret. The service principal creds necessary to retrieve the secret from the key vault are part of the configuration of the add-on. 

Azure Monitor Metrics are delivered via REST api. The REST api is accessed using a service principal name and password. These values are stored in a Key Vault secret. The service principal creds necessary to retrieve the secret from the key vault are part of the configuration of the add-on.  

The Azure Security Manager persona owns the event hub credentials and the service principal creds that do the "real work" (and are stored as secrets in Key Vault) as well as the service principal creds that can access the secrets. He shares the creds that can access the secrets (as part of the configuration of the add-on) with the Splunk Admin persona, but not the creds that do the "real work".

## Security Overview
[[images/security1.png]]