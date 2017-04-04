Configuration on the Azure side of things depends on the data input. Changes to configuration are immediate and require no restarts of either Splunk or the modular input / add-on.

## Activity Log
Activity Logs are configured to be Exported to an Event Hub (or storage account) at subscription-and-region scope. In the Azure portal, scroll to the bottom of the left nav and click the \> More Services button. Type "activity". Select "Activity Log" from the list. In the blade that pops up, select 'Export' from the menu.  

[[images/exportActivityLog1.PNG]]  

In the blade that pops up, select the subscription and regions that you want to export. Check the box to export to an event hub and set the retention that you want messages to stay in the event hub. If you're ingesting the messages into Splunk, they're picked up within a minute of appearance in the Event Hub. So you could think of the retention in event hub as a backup. Click the "Select a service bus namespace" button and configure the blade that pops up as shown.

[[images/exportActivityLog2.PNG]]  

## Diagnostic Logs
Diagnostic Logs are configured on a resource-by-resource basis. This configuration can be done in the portal, using the Azure CLI, PowerShell or code. I'll use the portal as an example here. This page gives full details: [How to enable collection of Diagnostic Logs](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs)

Find the Monitoring section of the blade of the resource you want to configure and click 'Diagnostic Logs':

[[images/diagnosticLogs1.PNG]]  

This will look different for different resources. Not all have Metrics and not all have Diagnostic Logs. Some have different options altogether or no Monitoring section at all. The blade that pops up is also resource specific. There will be a link or button for configuration of diagnostic logs such as the following example:

[[images/diagnosticLogs2.PNG]]  

Switch on diagnostics and go through the configuration of the event hub as shown:

[[images/diagnosticLogs3.PNG]]  

## Metrics

