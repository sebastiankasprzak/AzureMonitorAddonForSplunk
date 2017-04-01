# Installation on Ubuntu

* Download the SPL package from the packages folder of this repo.
* In Splunk Web, go to Manage Apps and click "Install app from file". Upload the file you just downloaded.
* You will get a message warning you that the add-on could not be initialized because dependencies are not included in the package. There are both Python and Node.js dependencies.

## Python Dependencies
* The alternative to doing the following steps manually is to use the shell script `am_depends.sh` in the packages folder.
* Open a terminal window to the VM and execute the following:
  * `apt-get update`
  * Install the latest version of pip. If you use the version that comes with "apt-get install python-pip", the installation of cryptography won't work.  
    Here's one way that works:  
      `wget https://bootstrap.pypa.io/get-pip.py`  
      `python get-pip.py`  
  * Install developer headers as follows:  (required for installation of cryptography)  
    `apt-get install build-essential libssl-dev libffi-dev python-dev`  
  * `pip install PyJWT`  
  * `pip install cryptography`
  * `pip install adal` 
  * `pip install splunk-sdk` 
  * `pip install futures` 
* The preceding steps brought the required packages to your VM. They need to be in the bin directory of the add-on because of the way that PYTHONPATH is defined by the Splunk environment.  
* In your terminal window:  
  * `cp /usr/local/lib/python2.7/dist-packages/six.py $SPLUNK_HOME/etc/apps/TA-Azure_Monitor_Metrics/bin`
  * `cp -R /usr/local/lib/python2.7/dist-packages/splunklib $SPLUNK_HOME/etc/apps/TA-Azure_Monitor_Metrics/bin`
  * `cp -R /usr/local/lib/python2.7/dist-packages/concurrent $SPLUNK_HOME/etc/apps/TA-Azure_Monitor_Metrics/bin`
  * `cp -R /usr/local/lib/python2.7/dist-packages/adal $SPLUNK_HOME/etc/apps/TA-Azure_Monitor_Metrics/bin`
  * `cp -R /usr/local/lib/python2.7/dist-packages/jwt $SPLUNK_HOME/etc/apps/TA-Azure_Monitor_Metrics/bin`
  * `cp -R /usr/local/lib/python2.7/dist-packages/dateutil $SPLUNK_HOME/etc/apps/TA-Azure_Monitor_Metrics/bin`

## Node.js Dependencies
* Open a terminal window on the Splunk Enterprise VM.
* If `npm` is not installed on the system (typical of a new Splunk Enterprise box):
  * `apt-get update`
  * `apt-get install npm`
* `cd $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin/app`
* `npm install`

## Last step
* Once dependencies are installed, the add-on will work by simply disable/enable on the Manage Apps page in Splunk Web. Or, you can restart Splunk.

