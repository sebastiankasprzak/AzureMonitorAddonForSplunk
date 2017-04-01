# Installation on Windows

* Download the SPL package from the packages folder of this repo.
* In Splunk Web, go to Manage Apps and click "Install app from file". Upload the file you just downloaded.
* You will get a message warning you that the add-on could not be initialized because dependencies are not included in the package. There are both Python and Node.js dependencies.

## Python Dependencies
* Open a command window and execute the following:
  * Install Python 2.7. Splunk comes with Python embedded, but not pip. Installing Python external to Splunk brings along pip. But not the latest version.
  * Install the latest version of pip. 
    Here's how: [Documentation](https://pip.pypa.io/en/stable/installing/)  
  * OR [upgrade pip in place](https://pip.pypa.io/en/stable/installing/#upgrading-pip)
  * `pip install PyJWT`  
  * `pip install cryptography`
  * `pip install adal` 
  * `pip install splunk-sdk` 
  * `pip install futures` 

## Node.js Dependencies
* Open a command window.  
* `cd $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin/app`
* `npm install`

## Last step
* Once dependencies are installed, the add-on will work by doing a disable/enable cycle on the Manage Apps page in Splunk Web. Or, you can restart Splunk.

