* Download the SPL package from the packages folder of this repo.
* In Splunk Web, go to Manage Apps and click "Install app from file". Upload the file you just downloaded.
* You will get a message warning you that the add-on could not be initialized because dependencies are not included in the package. There are both Python and Node.js dependencies.

## Python Dependencies
* The alternative to doing the following steps manually is to use the shell script `am_depends_mac.sh` in the packages folder.
* Open a terminal window to the VM and execute the following:
  * Install the latest version of pip.   
      `curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"`  
      `python get-pip.py`
  * `pip install python-dateutil -I`    
  * `pip install PyJWT`  
  * `pip install adal` 
  * `pip install splunk-sdk` 
  * `pip install futures` 
* The preceding steps brought the required packages to your VM. They need to be in the bin directory of the add-on because of the way that PYTHONPATH is defined by the Splunk environment.  
* In your terminal window:  
  * `cp /Library/Python/2.7/site-packages/six.py $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin`
  * `cp -R /Library/Python/2.7/site-packages/splunklib $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin`
  * `cp -R /Library/Python/2.7/site-packages/splunklib $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin/app`
  * `cp -R /Library/Python/2.7/site-packages/concurrent $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin`
  * `cp -R /Library/Python/2.7/site-packages/adal $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin`
  * `cp -R /Library/Python/2.7/site-packages/jwt $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin`
  * `cp -R /Library/Python/2.7/site-packages/dateutil $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin`

## Node.js Dependencies
* Open a terminal window on the Splunk Enterprise VM.
* If `npm` is not installed on the system (typical of a new Splunk Enterprise box), head over to https://nodejs.org/en/download/ to get the node.js pkg. It also installs npm.
* `cd $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin/app`
* `npm install`

## Last step
* Once dependencies are installed, the add-on will work by simply disable/enable on the Manage Apps page in Splunk Web. Or, you can restart Splunk.

