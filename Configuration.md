At the highest level, configuration is about setting up Splunk to monitor Azure assets within some scope. I'll call that the "scope of monitoring" or "monitoring target". Usually, I expect that the monitoring target of a data input instance will be all resources within an Azure subscription. But, as you'll see on the [[Configuration of Azure | configuration-of-azure]] page, configuration on the Azure side of things is extremely flexible. Your scope of monitoring for a particular data input instance could be as small as a single resource group or even a single resource.

Broadly speaking these configuration tasks are:

## Splunk
* Create and configure an instance of each desired data input (activity logs, diagnostic logs, metrics) for each subscription (monitoring target).

## Azure
* For the Activity Log, configure it to sink to an Event Hub.
* For Diagnostic Logs, configure each resource to collect logs and to sink to an Event Hub.
* For Metrics, add a tag saying which of the available metrics for that resource to send to Splunk. These tags can be modified any time and the changes will show up in Splunk's index immediately.
