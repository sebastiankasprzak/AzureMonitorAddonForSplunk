## version 1.2.4
* updated the RHEL installation script  

## version 1.2.3
* add ability to select which cloud you're operating in. Options are: Azure Public Cloud, Azure US Government, Azure China Cloud, Azure Germany Cloud. The selection is done by modification of an environment variable in azure_activity_log.sh and azure_diagnostics_logs.sh files.
* add sourcetype configuration for Activity Log messages. Currently, the configuration is source code based.

## version 1.2.2
* fix a bug with checkpoints when running multiple instances. 

Up until now, there was a single checkpoints file named simply checkpoints.json. When there are multiple instances running, all instances would look at this one file for their checkpoints, and, if running prod and test (for example) of the same event hub name (say, the one for activity log) there is a race condition as to which one would actually ingest messages. The solution is to append the name of the data input to the front of the checkpoints.json file, such as myDataInput_checkpoints.json. 

## version 1.2.0
* removed the auto-installation feature introduced in 1.1.0 due to customer feedback
* slight fix to installation script am_depends_ubuntu.sh

## version 1.1.0
* added a pseudo-data input (script) that auto-installs the add-on in an Ubuntu environment

## version 1.0.0
* a few small bugs
* conform more closely to Splunk Certified requirements

## version 0.9.10
* added a local cache of metric definitions. This eliminates a number of round trips. The file is bin/metricDefinitions.json. It may be deleted at any time and will be rebuilt from current definitions. The only time this would be necessary is if an existing metric-emitting resource added a metric.

## version 0.9.9
* encryption of key vault credentials

The SPNApplicationID and SPNApplicationKey values are replaced in inputs.conf with a mask (********). These values are stored in storagePasswords, i.e. passwords.conf. 
* use the sourcetype entered by user as default

If a resource type is not mapped to a sourcetype in sourcetypes.json, the default sourcetype, entered by the user in data inputs settings will be used.
* use the checkpoint directory provided by inputs.metadata
* refactor time window to support timedelta

Use datetime rather than time so timedelta's can be used to guarantee a timewindow is never <60 seconds. If the timewindow is <60 seconds, no values come from a requested metric.
