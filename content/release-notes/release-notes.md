---
uid: ReleaseNotes
---

# Release Notes

PI Interface for Emerson DeltaV Batch

**Version 5.1.0.6**

## Overview

The PI Interface for Emerson DeltaV Batch (EMDVB) creates batches in the PI Batch Database or Event Frames in PI AF database based on data from SQL data sources or EVT files. The interface automatically creates PI Tags and an AF Hierarchy to capture context around your process data.

The 5.1.0.6 release is a maintenance release that focuses on improving the stability and usability of the interface.

## Enhancements

There are no enhancements for this release.

## Fixes

This section lists items that were resolved or added in this release of PI Interface for Emerson Delta V.

| Work Item | Description                                                                     |
| :-------- | :------------------------------------------------------------------------------ |
| 22132     | History recovery is fixed to prevent infinite loop scenario when querying for SQL data. In addition, fixed time as double to string time conversions There was a millisecond precision error converting the time stored as doubles to a time string. |
| 22133     | Attribute values referencing other event frames are captured regardless of the order event frames are created. |
| 22140     | Unirecord data sources are now included in unirecord imports and exports. |
| 22153     | Restore DESCRIPT handling in phase step logic. |
| 22156     | Cache start and end times can no longer be permanently altered by arbitration events. |
| 22163     | SQL Native client print message was disabled for Oracle based interfaces. |
| 22171     | Changed the Batch-list management algorithm to improve event processing accuracy (prevent missed batches). | 
| 22172     | When removing an interface from PI Event Frames Interface Manager, it will also remove any associated services. |
| 22181     | When adding an interface to PI Event Frames Interface Manager, the instance ID will be initialized as the same value of interface ID. |
| 22209     | Interface will no longer have a delay in processing a batch when the local time is greater than GMT. |
| 22211     | MONITORTAGWINDOW now defaults to 0, meaning monitor tag counts don't get trimmed to the most recent <MONITORTAGWINDOW> days of activity and roll over at INT_MAX unless MONITORTAGWINDOW is deliberately set. |
| 22216     | Interface ID has been added to the message logs in order to uniquely identify log message.
| 22218     | All generated unirecords will have the placeholder [TIMESTAMP] have the format "YYYY-MM-DD" for a SQL source and "YYYY/MM/DD" for non SQL source like EVT files.
| 22221     | Monitor tags now accurately reflect the number of batches and their child events. |
| 22224     | Bifconfig properly creates new default virtual user service without errors. |
| 22235     | Interface configuration for RST and RET reads UnitedStates format standard. |
| 22245     | The unit procedure batch id attribute is controlled by the unit procedure recipe template batchid. |
| 22246     | BifConfig does not allow older interfaces to edit health tags. |
| 22249     | All batch interfaces remove passwords from INI file regardless of parameter capitalization. |
| 22250     | Merging issue causes unit procedure and operation not to close. |
| 22260     | Batch event frames no longer merge event frames when merging is disabled and unique ids don't match. |
| 22268     | All RST and RET within the configuration will be parsed as US format. Fix in current development branch and in 4.3.x.x Branch. |
| 22275     | A check that verifies that a Procedure Event Frame and a Unit Procedure Event Frame are both generated by the same interface instance before linking them together. |
| 22283     | The Event log source is created during the interface install step. |
| 22464     | For interfaces with a version 5.0.0 or greater, PI Event Frames Interface manager nows tail the windows event viewer instead of PI Message log. |
| 23177     | BifConfig now stores RST and RET as UTC Note that they can be edited in a local friendly time string and read into the interface correctly. When written by the configuration program, they will write the times out as UTC and a local time string as a comment. |
| 23299     | EMDVB fetches SQL data with greater efficiency. EMDVB gathers SQL data for lists of batches rather than querying each batch's data individually, and reuses the same SQL connection for all queries. |
| 24361     | All boost library calls were replaced with native C++ and STL functions. |
| 24661     | Boost is no longer used for JSON processing. Microsoft Net library replaces it. |
| 24781     | The interface setup kit is using the same GUID for all the interface. This causes trouble when installing another batch interface on the same machine. Fixed to use different GUID for each interface. |
| 24847     | SQL Native Client is no longer supported, and is now replaced with OLEDB for all supported batch interfaces. |
| 25811     | PI data server collectives and PI buffering to multiple PI data servers is now supported. |
| 26756     | With the release of version 5, if you have a batch interface supported batch database, it will no longer be able to write to PIBatch Database. Version 5  only supports Event Frames Customers who need to write to PIBatch. The database needs to stay with Version 4.x.x.x Batch Interfaces. |
| 67289     | UniRecord exports now include all UniRecord fields. |
| 67298     | Event sorting is faster and memory consumption is better managed during event queuing. |
| 67926     | Interface will not allow Batch events with a zero start time. |
| 68207     | BifConfig will now store SCAN values as low as one second without complaint. |
| 68907     | Default account to setup interface service is now Default Virtual User (NT Service/<Interface Instance Name>). |

## Known Issues

There are no known issues for this release.

## System Requirements

### Operating Systems

This interface is a 64-bit application.

| Platform  | 64-bit Application  |
| :-------- | :------------------ |
| Windows Server 2022 (64-bit) | Yes |
| Windows Server 2019 (64-bit) | Yes | 
| Windows Server 2016 (64-bit) | Yes | 
| Windows Server 2012 R2 SP1 (64-bit) | Yes | 
| Windows Server 2012 (64-bit) | Yes | 
| Windows 11 (64-bit) | Yes | 
| Windows 10 (64-bit) | Yes | 
| Windows 8.1 (64-bit)| Yes | 
  
## Distribution Kit Files

| Product   | Software Version  |
| :-------- | :------------------ |
| Microsoft OLE DB Driver | 19.2.0 |
| Microsoft Visual C++ 2015-2019 Redistributable (x86) | 14.21.27702 |
| Microsoft Visual C++ 2015-2019 Redistributable (x64) | 14.21.27702 |
| PI AF Client 2018 SP3 Patch 3 | 2.10.9.593 |
| PI Interface for Emerson DeltaV Batch (EMDVB) | 5.1.0.6 |
| PI Network Subsystem Support (PINS)* | 3.4.435.538 |
  
*The PI Network Subsystem Support (PINS) component is not displayed on the installation welcome screen if the PI Data Archive is installed already.

### Installation and Upgrade

The PI Interface for Emerson DeltaV Batch can be installed or upgraded using the PI Interface for Emerson DeltaV Batch installation kit, EMDVB_5.1.0.6_.exe. This installation kit can be obtained by using the How to Download Products link listed in the OSIsoft Customer Portal How To's list. This list is located on the [OSIsoft Customer Portal](https://my.osisoft.com/).

For additional information regarding the PI Interface for Emerson DeltaV Batch installation, please see the Installation instructions portion of the PI Interface for Emerson DeltaV Batch (PIBatchGuide) User Guide. This user guide is available for download from the [OSIsoft Customer Portal](https://my.osisoft.com/).

### Uninstalling PI Web API

The PI Interface for Emerson DeltaV Batch Interface can be uninstalled using the *Programs and Features* list accessible from the *Windows Control Panel*. After accessing the Programs and Features list, select the entry named *PI Interface for Emerson DeltaV Batch (EMDVB)* and then select *Uninstall* from the menu.

## Security information and guidance

OSIsoft is [committed to releasing secure products](https://docs.osisoft.com/bundle/security-commitment-and-disclosure-standards/page/securitycommitmentanddisclosurestandards.html). This section is intended to provide relevant security-related information to guide your installation or upgrade decision.  

OSIsoft [proactively discloses](https://docs.osisoft.com/bundle/security-commitment-and-disclosure-standards/page/securitycommitmentanddisclosurestandards.html#vulnerability-communication) aggregate information about the number and severity of security vulnerabilities addressed in each release. The tables below provide an overview of security issues addressed and their relative severity based on [standard scoring](https://docs.osisoft.com/bundle/security-commitment-and-disclosure-standards/page/securitycommitmentanddisclosurestandards.html#vulnerability-scoring). 

There are no security vulnerabilities in this release. 