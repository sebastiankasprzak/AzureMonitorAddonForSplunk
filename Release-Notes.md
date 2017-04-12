Installation tests on Mac OS X are not complete. More work on installing dependencies is needed.

Installation tests on Windows and Ubuntu 14.04 are all good.

## version 0.9.9
* encryption of key vault credentials

The SPNApplicationID and SPNApplicationKey values are replaced in inputs.conf with a mask (********). These values are stored in storagePasswords, i.e. passwords.conf. 
* use the sourcetype entered by user as default

If a resource type is not mapped to a sourcetype in sourcetypes.json, the default sourcetype, entered by the user in data inputs settings will be used.
* use the checkpoint directory provided by inputs.metadata
* refactor time window to support timedelta

Use datetime rather than time so timedelta's can be used to guarantee a timewindow is never <60 seconds. If the timewindow is <60 seconds, no values come from a requested metric.
