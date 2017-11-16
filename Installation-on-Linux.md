* Download the SPL package from the packages folder of this repo.
* In Splunk Web, go to Manage Apps and click "Install app from file". Upload the file you just downloaded.
* You will get a message warning you that the add-on could not be initialized because dependencies are not included in the package. There are both Python and Node.js dependencies.

## Python Dependencies
* The alternative to doing the following steps manually is to use the shell script `am_depends_ubuntu.sh` (or `am_depends_rhel.sh`) in the packages folder. I find the best way to do it is:
  * `sudo su`
  * `cd ~`
  * `./am_depends_ubuntu.sh`
  * `exit`  
* For illustration purposes, these are the steps if you want to do it manually in Ubuntu. Open a terminal window to the VM and execute the following:
  * `apt-get update`
  * Install the latest version of pip. If you use the version that comes with "apt-get install python-pip", the installation of cryptography won't work.  
    Here's one way that works:  
      `wget https://bootstrap.pypa.io/get-pip.py`  
      `python get-pip.py`  
  * Install developer headers as follows:  (required for installation of cryptography)  
    `apt-get install build-essential libssl-dev libffi-dev python-dev` 
  * `pip install six -I`
  * `pip install adal` 
  * `pip install splunk-sdk` 
  * `pip install futures` 
* The preceding steps brought the required packages to your VM. They need to be in the bin directory of the add-on because of the way that PYTHONPATH is defined by the Splunk environment.  
* In your terminal window:
  * `export SPLUNK_HOME=/opt/splunk`
  * `export PYTHON_SITEPACKAGES=/usr/local/lib/python2.7/dist-packages`
  * `cp $PYTHON_SITEPACKAGES/six.py $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin`
  * `cp -R $PYTHON_SITEPACKAGES/splunklib $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin`
  * `cp -R $PYTHON_SITEPACKAGES/concurrent $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin`
  * `cp -R $PYTHON_SITEPACKAGES/adal $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin`
  * `cp -R $PYTHON_SITEPACKAGES/jwt $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin`
  * `cp -R $PYTHON_SITEPACKAGES/dateutil $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin`

## Node.js Dependencies
* Open a terminal window on the Splunk Enterprise VM.

### Ubuntu 14+
* If `npm` is not installed on the system (typical of a new Splunk Enterprise box):
  * `curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -`
  * `apt-get install -y nodejs`
* `cd $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin/app`
* `npm install`

### RHEL 7
* If `npm` is not installed on the system (typical of a new Splunk Enterprise box):
  * curl --silent --location https://rpm.nodesource.com/setup_6.x | sudo bash -
  * yum -y install nodejs
* `cd $SPLUNK_HOME/etc/apps/TA-Azure_Monitor/bin/app`
* `npm install`

## Last step
* Once dependencies are installed, the add-on will work by simply disable/enable on the Manage Apps page in Splunk Web. Or, you can restart Splunk.

