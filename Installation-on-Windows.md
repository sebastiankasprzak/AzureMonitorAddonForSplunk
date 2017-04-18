* Download the SPL package from the packages folder of this repo.
* In Splunk Web, go to Manage Apps and click "Install app from file". Upload the file you just downloaded.
* You will get a message warning you that the add-on could not be initialized because dependencies are not included in the package. There are both Python and Node.js dependencies.
* We need both pip for Python package installation and npm for Node.js package installation. This is why we're installing Python and Node. If you already have pip & npm, we don't need to install Python & Node.

## Python Dependencies
* Open a command window and execute the following:
  * Install Python 2.7. Here's the [link](https://www.python.org/downloads/release/python-2712/).
  * `pip install` puts files into `c:\python27\lib\site-packages` regardless of where you execute it from.
  * `pip install adal` 
  * `pip install splunk-sdk` 
  * `pip install futures` 

## Node.js Dependencies
* Install Nodejs from [here](https://nodejs.org/en/download)  
* Open a command window.  
* `cd $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin/app`
* `npm install`

## Last step
* Once dependencies are installed, the add-on will work by doing a disable/enable cycle on the Manage Apps page in Splunk Web. Or, you can restart Splunk.

