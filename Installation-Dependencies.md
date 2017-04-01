# Installation of Dependencies

Azure Monitor Add-on For Splunk has two basic functions: logs and metrics. Logs come from Event Hubs and metrics come from a REST API. Historically, the metrics part was written first and in Python. Node.js was found to be preferable when working with Event Hubs / Logs.  

The packages in this repo do not contain the dependency packages for either language environment, so they must be installed after the SPL package is installed into your Splunk environment.  

[[Windows | installation-on-windows]]  
[[Linux | installation-on-linus]]