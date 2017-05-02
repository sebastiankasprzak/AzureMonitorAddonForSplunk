In version 1.1.0, a special [scripted input](http://docs.splunk.com/Documentation/Splunk/latest/AdvancedDev/ScriptedInputsIntro) was added to the 3 existing inputs. The job of this scripted input is to install Python and Node.js dependencies for this add-on. It executes upon Splunk restart. Each step tests to see if it's needed before executing. If the script has run successfully once, it takes less than 10 seconds to execute these tests. The progress of the script may be tracked with "index=_internal sourcetype=ta:installer". There are several lines in the log ("logging break") that are there to avoid the 256 line maximum enforced by default in Splunk.

The implementation of this scripted input involves two artifacts:
* a new stanza in default/inputs.conf
* a shell script - bin/linux_dependencies.sh

When the SPL is initially installed, Splunk will still issue the warning about inability to initialize the add-on: 
```
Unable to initialize modular input "azure_monitor_metrics"  
defined inside the app "TA-Azure_Monitor":  Introspecting  
scheme=azure_monitor_metrics: script running failed  
(exited with code 1).  
```

A Splunk restart executed by root at a shell prompt (NOT Server Controls restart) is required for the script to run successfully. It runs as root.  Disable/Enable the add-on after the script completes to clear the warning.

At a high level, the script does the following:
* apt-get update
* install node.js + npm
* install the node.js packages needed by the add-on
* install python pip.
* install various python packages required for building cryptography module
* install Azure Directory Authentication Library (adal)
* install splunk-sdk
* install futures (a Python package that implements parallel processing)

The script takes about 5 minutes to run. If you are tracking (index=_internal sourcetype=ta:installer), the last line of the script will say "Logging break - copy libraries to add-on folder". At this point, disable/enable the add-on and proceed with configuration of the data inputs.