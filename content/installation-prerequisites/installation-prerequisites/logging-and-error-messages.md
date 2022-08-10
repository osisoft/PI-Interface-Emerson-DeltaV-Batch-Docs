---
uid: BIF_LoggingAndErrorMessages
---

# Logging and error messages

<!-- Static topic. No modifications usually required -->

The interface logs operational messages during interface startup, data collection and recovery. Additional messages are logged if you enable debugging. To view messages, open Windows Event Viewer on the interface’s installed machine and go to the Applications and Services Logs. Locate the log using the generic interface name. The management of the logs can be done through the Windows Event Viewer.  

To enable debug output for troubleshooting, launch PI Event Frames Interface Manager, select your interface instance, and go to the Operational Settings tab.

**Operational settings**

Local debug messages (/DB=<#>)

Specifies level of detail for logging as follows: 

* 0: Log errors and warnings (default) 

* 1: Log errors, warnings and major successes 

* 2: Log all messages 

* 3: Log all messages including Unirecord diagnostic message

**Command line parameter reference**

/db =[#] 

(Optional) Enabled debugging output: 

* 0: Log only errors and warnings (default) 
* 1: Log errors, warnings and major success messages 
* 2: Log all messages (most verbose
* 3: Log all messages including Unirecord diagnostic message





