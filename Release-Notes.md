Installation tests on Windows, Mac and Ubuntu 14.04 are all good.

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
