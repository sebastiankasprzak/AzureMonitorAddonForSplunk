Configuration on the Azure side of things depends on the data input. Changes to configuration are immediate and require no restarts of either Splunk or the modular input / add-on.

## Activity Logs
At a high level, Activity Logs are configured to be Exported to an Event Hub (or storage account) at subscription-and-region scope. In the Azure portal, scroll to the bottom of the left nav and click the > More Services button. Type "activity". Select "Activity Log" from the list. In the blade that pops up, select 'Export' from the menu.
[[images/exportActivityLog1.PNG]]

## Diagnostic Logs

## Metrics