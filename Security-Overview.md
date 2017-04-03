Azure Monitor Logs (Activity and Diagnostic) are delivered via Event Hubs. An event hub is accessed using a policy name and key. These values are stored in a Key Vault secret. The creds necessary to retrieve the secret from the key vault are part of the configuration. 


Azure Monitor Metrics are delivered via REST api. 