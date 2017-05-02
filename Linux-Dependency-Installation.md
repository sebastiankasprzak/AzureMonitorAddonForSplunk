In version 1.1.0, a special [scripted input](http://docs.splunk.com/Documentation/Splunk/latest/AdvancedDev/ScriptedInputsIntro) was added to the 3 existing inputs. The job of this scripted input is to install Python and Node.js dependencies for this add-on. Each step tests to see if it's needed before executing. If the script has run successfully once, it takes less than 10 seconds to execute these tests. The progress of the script may be tracked with "index=_internal sourcetype=ta:installer".

The implementation of this scripted input involves two artifacts:
* a new stanza in default/inputs.conf
* a shell script - bin/linux_dependencies.sh

When the SPL is initially installed, Splunk will still issue the warning about inability to initialize the add-on: 
```
Unable to initialize modular input "azure_monitor_metrics" defined inside the app "TA-Azure_Monitor"
```

A Splunk restart is required for the script to run successfully. It runs as root.  

At a high level, the script does the following:
* apt-get update
* install node.js + npm
* install the node.js packages needed by the add-on
* install python pip.
* install various python packages required for building cryptography module
* install packages required by splunk-sdk
* install Azure Directory Authentication Library (adal)
* install futures (a Python package that implements parallel processing)
 