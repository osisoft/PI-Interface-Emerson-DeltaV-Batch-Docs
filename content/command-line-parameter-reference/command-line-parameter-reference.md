---
uid: BIF_CommandLineParameterReference
---

# Command line parameter reference

<!-- Customized for DeltaV. Commented out commands don't apply to DeltaV -->

To configure an interface, you use the PI Event Frames Interface Manager, which maintains the files that contain batch interface settings. This appendix describes the command line settings and is provided for troubleshooting purposes.
    
**Note:** To ensure that settings files are formatted correctly, always use PI Event Frames Interface Manager to configure settings. Do not edit settings files manually.

The following table is a compilation of the command line settings for all the OSIsoft batch framework interfaces. Some settings are specific to an interface. To list the settings supported by your interface, invoke its executable at the command line, specifying the -? flag.

## Available command line parameters

The following headings describe each command line parameter available.

### `/abto =<#days>` 

(Optional) Specifies how long, in addition to the CACHETIME setting, the interface waits before closing a batch for which no end event has arrived. When an abandoned batch is closed, the interface uses the timestamp of its last event as the end time and logs an "Abandoned batch found" message. Default is 100 days, minimum is .042 days (approximately one hour), and maximum is 365 days.

### `/adu =[true | false]`

(Optional) Enable the creation of unit batches for recipes in units that are allocated at the phase level rather than the unit batch level. By default, the interface requires the unit name to be present in the unit batch start event. When you enable /adu, the interface creates the unit batch and defers setting the unit name until the phase-level allocation event arrives.

<!-- 

### `/batchrcp =[true | false]` 

(ABB only) Collect full task hierarchy. By default, the interface collects four levels. For details, refer to ABB 800xA batch start and stop events. 

-->

### `/bidm =<list>` 

(Optional) Override the incoming batch ID by selecting a substring. Specify one or more masks composed of text and wildcards, to be used to compose the desired batch ID from the contents of the source BatchID field. The resulting batch ID is used for the Batch ID field of the top-level procedure and for the [BATCHID] placeholder. By default, the batch ID field in unit procedures contains the full batch ID from the data source. To use the truncated batch ID instead, configure the TBID setting. 

Valid wildcards are as follows:

| Wildcard | Description |
| -------- | ----------- |
| # | Single digit numerical value, 0-9 |
| @ | Single alpha character, a-z, A-Z |
| ? | Any single symbol |
| ! | Repeat the previous mask symbol |
| * | Any set of symbols |

#### Wildcard use example

If the incoming Batch ID is: `lot30112 / 90dev123 / 12345stp / ld567`

The following list shows example masks and resulting data.

| Mask | Result |
| ---- | ------ |
| "######" | 30112 |
| "##@!" | 90dev |
| "*###@!" | lot30112 / 90dev |
| "@@@@, #8dev4, #!" | 30112 |

In the last example, the first and second masks do not match, so the third mask is used. 

### `/cachetime=<days>` 

(Optional) Batches are cached in memory to enable the interface to capture events sent by the BES after the batch has closed. This setting specifies how long (in days) completed batches are cached. To specify fractions of a day, use decimal values. For example, /cachetime=7.5 releases completed batches when their end time is more than 7 days and 12 hours from the current time. The default value is 1 day, minimum is .042 days (approximately one hour), and maximum is 60 days.

### `/dac` 

(Optional) Disable arbitration counters: directs the interface to release a unit on the first resource release event even if the number of acquire events is higher than number of release events. By default, the interface requires the number of acquire and release events for a unit to be the same.

### `/damcae` 

(Optional) Ignore events from a DeltaV Event Chronicle (alarms & events) data source when creating or checking PI Module Database objects. If the module path defined for an AlarmTag[#].Alias entry contains the root node symbol ($), the interface checks the module path regardless of whether this option is enabled.

### `/datasec=<string>`

(Optional) Specifies the security settings to be assigned to interface-generated tags. For PI Data Archive 3.4.375.99 or earlier, use owner, group, world format. Example: /datasec="o:rw g:r w:r" For PI Data Archive 3.4.380.36 or later, specify an access control list (ACL). 

Example: 

```text
/datasec="piadmin: A(r,w) | PIEngineers: A(r)"
```

### `/db =[#]` 

(Optional) Enabled debugging output:

* 0: Log only errors and warnings (default)
* 1: Log errors, warnings and major success messages
* 2: Log all messages (most verbose)

### `/dpretc` 

(Optional – event frames only) Disable propagation of referenced elements to children. By default, the interface propagates each event frame element reference to its children event frames.

### `/enabledmonitortags =<TAG>]`

Indicates which [monitor tags](xref:BIF_MonitorTagSetupTab) are enabled. Each enabled tag consumes a license, but disabled tags do not. You can enable multiple monitor tags by separating each one with a comma-separated list. For example:

```text
/enabledmonitortags=BATCHSTATUS,BATCHPROCESSORSTATUS,BATCHLISTCOUNT,EQUIPMENTCOUNT,TAGLISTCOUNT,TAGAELISTCOUNT,EVENTREADCOUNT,ERRORCOUNT,SOURCEUNITCOUNT,PIUNITCOUNT,SOURCEPHASEMODCOUNT,PIPHASEMODCOUNT,SOURCEBATCHCOUNT,PIBATCHCOUNT,SOURCEUNITBATCHCOUNT,PIUNITBATCHCOUNT,SOURCESUBBATCHCOUNT,PISUBBATCHCOUNT,SOURCEPROPERTYNODECOUNT,PIPROPERTYNODECOUNT,SOURCEPROPERTYEVENTCOUNT,PIPROPERTYEVENTCOUNT,SOURCETAGCOUNT,PITAGCOUNT,SOURCETAGEVENTCOUNT,PITAGEVENTCOUNT,SOURCETAGALIASCOUNT,PITAGALIASCOUNT,CACHEDBATCHCOUNT,OPENBATCHCOUNT,SOURCEREADTIME,TAGCACHETIME,BATCHCACHETIME,EQUIPMENTCACHETIME,BATCHSYNCTIME,TAGSYNCTIME,EQUIPMENTSYNCTIME,TOTALTIME,WAITINGFOREQUIPMENTUB,NUMBEROFWORKORDERS,NUMBEROFOPENWORKORDERS,WORKORDERQUERYTIMEAVG
```

For more information about each tag available, see [Monitor tag reference](xref:BIF_MonitorTagSetupTab#monitor-tag-reference).

Additionally, you can enable or disable all tags using the `ALL` or `NONE` options:

```text
/enabledmonitortags=ALL
/enabledmonitortags=NONE
```

### `/equipmentXML =<filepath>` 

(Optional) Specifies the location of the DeltaV-generated equipment hierarchy XML file. The EMDVB interface uses this reference data to locate missing ProcessCell field by searching based on the combination of Area and Unit fields. Valid only when a DeltaV AE SQL datasource is defined. 

Example: 

```text
/EquipmentXML="C:\DeltaV\Equip.xml"
```

### `/failoverID =<string>`

(Optional) Configure a unique failover ID for the interface instance. Must be used with the `/failover` parameter.

Example: `/FailOverID="intf1"`

### `/failovertag =<tag name>`

(Optional) Specifies the PI tag to be used to track the primary interface instance. Must be used with the `/failoverID` parameter.

Example: `/failovertag="Batch_FailoverTag"`

### `/host =host:port`

(Required) Specifies the PI Data server or PI Collective where data is to be stored. Host is the IP address or domain name of the server node. Port is the port number for TCP/IP communication. The port is always 5450.

Examples: 

* `/host=marvin`
* `/host=marvin:5450`
* `/host=206.79.198.30`
* `/host=206.79.198.30:5450`

### `/id =<identifier>`

(Required) Specify a one- to nine-number identifier for the interface instance. Assigned to the Location1 attribute of tags that the interface instance updates.

<!-- ### `/includeincompletedata`

(Optional) Enables the collection of all unit procedures without and associated UNIT. Without this option unit procedures that do not have phase state that associated with a particular UNIT will not be shown as events in PI AF. -->

### `/inifile =<path>`

(Optional) Override the default location and name for the initialization file. By default, the .ini file resides in the interface installation directory and has the same file name and the .bat file.

### `/link =<AF element path>`

(Deprecated, see `/readlink` and `/writelink`.) Combine event frames from different interface instances. Useful when you have an MES controlling multiple BESs. Configure an interface instance for each BES, specifying the same linkage element. The BES interface instances create event frame references under the MES event frames that refer to the BES interface instances. For Emerson Syncade systems, the AutomationBatchID field must match the batchID of the batch created by the BES.

### `/maxqtf =<days>`

(Optional) Sets the maximum number of days for which a query can return data. Used to break a large query into a set of smaller queries, to ensure that the system does not run out of memory. The value can be fractional.

* Minimum: 0.001
* Maximum: 180
* Default: 30
  
### `/maxstoptime =<seconds>`

(Optional) Specifies (in seconds) the maximum time allowed for the interface to properly shutdown. If shutdown takes longer than the specified time, the interface is forced to terminate immediately. Default: 120 seconds

### `/merge`

(Optional) Enable merging of multiple source batches with same ID. The original data for each batch merged is stored in PI properties under a node named using the ID of the original batch. The data includes the original batch ID, start time (UTC), end time (UTC), product and formula name. The interface merges only batches that are cached in local memory. The time frame for merging is configured using the `/cachetime` switch.

If the IDs of the batches you want to merge are different, use the `/bidm` flag to override incoming IDs.

Example: Given the following five batches running within the cache time frame.

* Test12345_1
* Test_12345_2
* CleaningTest
* USPO12345_test
* CleaningTest

With merging enabled, only the CleaningTest batches are merged. To merge the other three batches, which have IDs containing the string "12345", specify `/bidm=######`.

### `/mode =<mode>` 

(Optional) Valid modes are as follows:

* **Realtime:** (Default) Real-time data collection. If a recovery start time is specified (`/rst`), the interface recovers data before starting real-time collection.

* **Stat:** Statistics mode. Compare source data with the corresponding PI System batch data. The interface does not write to or modify any data PI batch data. On completion, the interface reports results and stops.

* **Delete:** Delete batch data from PI archives for specified period, leaving data from all other sources intact. Use only if the interface is unable to synchronize source batch data with the PI System. Must be used in conjunction with the recovery mode switches (`/rst` and `/ret`).

* **NoData:** Newly-added tags, units and modules are indexed (referenced) in the primary PI archive, but older archives do not have entries for these modules, units and tags. In NoData mode, the interface creates modules, units, tags and tag aliases without processing batch data and writing events to the tags. To recover batch data for a period prior to the one in the primary archive, you must reprocess older archives with the offline archive utility. Manual archive reprocessing creates indexes for newly-added units, modules, tags. Always run the interface in this mode before writing new batch data to older PI archives (that is, archives other than the primary archive).

### `/monitortagwindow =<days>`

(Optional) Monitor tag time window in days. Most [monitor tags](xref:BIF_MonitorTagSetupTab) show a sum of events over a number of days. This setting allows the size of the window to be adjusted. The default value is one day.

### `/mop`

(Optional) Merge identically named operations under the same parent unit procedure. The start time of the combined operation is the start of the earliest operation and the end time is the end time of the latest or longest operation that was merged.

### `/mup`

(Optional) Merge identically named sequential unit procedures running on the same unit into a single unit procedure. Unit procedures are not merged if the unit was used by another recipe between candidates for merging. The start time of the resulting merged unit procedure is the start of the earliest unit procedure, and the end time is the end time of the latest or longest unit procedure that was merged.

### `/noarbitration`

Create unit batches based solely on source batch recipe data. For use when the source Batch Executive System (BES) provides batch data without equipment arbitration.

### `/ns[=lang]`

(Optional) Perform numerical conversions using the specified language's conventions. Useful when the numerical conventions differ from the default settings (for example, comma instead of decimal point). Default is "English_UnitedStates". If you omit the language parameter, the interface uses the "Regional and Language Options" settings in effect for the interface node.

Language types and abbreviations:

* chinese chinese-simplified (chs)
* chinese-traditional (cht)
* czech (csy)
* danish (dan)
* belgian, dutch-belgian (nlb)
* dutch (nld)
* australian, english-aus (ena)
* canadian, english-can (enc)
* english english-nz (enz)
* english-uk (uk)
* american, american-english, english-american, english-us, english-usa, (enu) (us) (usa)
* finnish (fin)
* french-belgian (frb)
* french-canadian (frc)
* french (fra)
* french-swiss (frs)
* german-swiss, swiss (des)
* german (deu)
* german-austrian (dea)
* greek (ell)
* hungarian (hun)
* icelandic (isl)
* italian (ita)
* italian-swiss (its)
* japanese (jpn)
* korean (kor)
* norwegian-bokmal (nor)
* norwegian norwegian-nynorsk (non)
* polish (plk)
* portuguese-brazilian (ptb)
* portuguese (ptg)
* russian (rus)
* slovak (sky)
* spanish (esp)
* spanish-mexican (esm)
* spanish-modern (esn)
* swedish (sve)
* turkish (trk)

### `/piconnto =<seconds>` 

(Optional) Override the default SDK setting for PI connection timeout.

### `/pidato =<seconds>`

(Optional) Override the default SDK setting for PI data access timeout.
### `/pipswd =<password>`

(Optional) Specify the user password to be used to connect to the PI Data Archive. By default, the interface uses PI trusts for authentication.

### `/piuser =<name>`

(Optional) Specify the user name to be used to connect to the PI Data Archive. By default, the interface uses PI trusts for authentication.

### `/print =<filename>` 

(Optional) Prints the results of first scan to specified text file. The results include the batch tree, tag list, and equipment tree. Used for troubleshooting.

### `/ps =pointsource` 

Specifies the point source for the points maintained by the interface.
### `/ptsec =<string>` 

(Optional) Specifies the access security settings to be assigned to interface-generated tags. For PI Data Archive version 3.4.375.99 or earlier, use owner, group, world format.

Example:

```text
/ptsec="o:rw g:r w:r"
```

For PI Data Archive version 3.4.380.36 or later, specify an access control list (ACL). 

Example:

```text
/ptsec="piadmin: A(r,w) | PIEngineers: A(r)"
```

### `/ras =<startstr, stopstr>`

(Optional) Directs the interface to use the "Report" event to create phase steps under active phase states. The phase step name and start/stop events are obtained from the "Descript" column. The start and stop strings must start in the same position in the data source and must not be the first characters in the "Descript" column. The phase step name is derived from the characters preceding the start/stop text. Specify the strings in a double-quoted comma-separated list, as shown in the example below.

Example: `/ras="-STRT, -STOP"`

If the Descript Column contains TEST123-STRT-B, the interface generates a phase step named "TEST123" under the currently active phase state. Open phase steps are closed by the end of the parent operation and not by the end of parent phase or phase state.

### `/readlink= <AFelementpath>`

Combine event frames from different interface instances. For an MES controlling one or more BES systems, configure `/readlink` on the MES interface and configure an interface instance for each BES, specifying the same linkage element in the BES `/writelink` setting. The BES interface instances will then create event frame references under the MES event frames that refer to the BES event frames. For Emerson Syncade systems, the AutomationBatchID field must match the batchID of the batch created by the BES.

For a BES interface controlling one or more MES systems, configure `/readlink` on the MES interface and configure an interface instance for each BES, specifying the same linkage element in the BES `/writelink` setting. The MES interface will then create event frame references under the BES event frames that refer to the MES event frames. Link templates must also be configured to define which events specify a link.

### `/restef`

(Optional) Enables an event frame with references to inherit security settings from its primary reference element.

### `/ret =<datetime>`

(Optional) Specifies the end time for data recovery. The interface recovers batches that start before the specified time, including batches that end after the specified end time. Specify the time using the interface node format and time zone.

### `/retry =<seconds>`

(Optional) Specifies how often the interface retries a failed attempt to write data. The default is 60 seconds.

### `/retryto =<seconds>`

Specifies how long the interface retries a failed attempt to write data before timing out. By default, the interface never times out. If you configure a timeout setting, be advised that you risk losing data.
### `/rst =<datetime>`

(Optional) Specifies recovery start time. The interface recovers batches that start after the specified time, as well as batches that start before the specified time but end after it. Specify the time using the interface node format and time zone.

### `/rti`

Remove trailing index from Recipe fields. Applicable to Procedure, Unit Procedure, and Operation Recipe fields. Emerson EVT data source only.

### `/scan =<seconds>`

(Optional) Specifies, in seconds, how often to scan the data source for new data. The default is 60 seconds. A scan that returns a large amount of data can cause the interface to skip the subsequent scan.

### `/singlerun` 

(Optional) Perform one scan and stop.

### `/smp ="equipment path"`

(Optional) Specifies an alternate PI Module path or PI AF element path for a particular equipment hierarchy. By default, the interface scans starting at the root level. Use the following syntax:

`\\<RootModule>\<SubModule>\<…>`

### `/sqlconnto =<seconds>` (DeltaV SQL only)

(Optional) Override the default SQL timeout setting (60 seconds).

### `/sqldato=<seconds>` (DeltaV SQL only)

(Optional) Override the default SQL data access timeout setting (100 seconds).

### `/swaptime =<seconds>`

(Optional) Specifies, in seconds, how long the current primary interface must be unavailable before failover occurs. Default: 300 seconds.

### `/tbid`

(Optional) Use the truncated batch ID in the batch ID field of unit procedures. Incoming batch IDs are reformatted using the mask defined in the `/bidm` parameter.

### `/tbse`

(Optional) True Batch Start End (`/TBSE`) is a mechanism used to determine when the PI Batch initially started. `/TBSE` is also referred to as the recipe-based start/end or the true start and end time and is set to FALSE by default. This tool is helpful if you have reporting software, such as rtreports, and require a precise start time in your reports. It is intended for batches with S88 recipe types: Procedure, Unit Procedure, Operation, and Phase.

When `/TBSE = true` in the .ini configuration file, the interface uses top level recipe start/end events for creating batch objects. When processing a batch, you begin first with a batch event and followed by a procedure event. The interface uses the start time of the initial batch event prior to the procedure start event to indicate the start of the batch. 

When a batch event ends, usually through a BATCH STOP event, the PROCEDURE COMPLETE State Change event timestamp lists the specific end time.

**Note:** We do not recommend configuring both the `/TBSE` and the Use Batch Recipe (`/UBR`) command line parameters to TRUE at the same time. These parameters are independent from one another and are best utilized when run in separate configurations.

If both `/TBSE` and `/UBR` are set to TRUE, it is likely that `/TBSE` will overwrite the start and end times of the batch.

### `/ts=GMT | LCL` 

(Optional) Specifies how the interface interprets event timestamps from an SQL data source. Options are local time or GMT. Default is GMT.

### `/ubr`

Use Batch Recipe (`/UBR`) is a mechanism that allows the interface to enable or disable the use of the batch recipe view to generate PI Batch database objects.

You can configure `/UBR` in the .ini configuration file, on the command line, or on the Batch Setup tab in the PI Event Frames Interface Manager. By default, `/UBR` is set to false in the Emerson batch interfaces. 

When `/UBR = false`, the interface uses STATE CHANGE logic to control the start and end of event frames. Example State Change messages are RUNNING, REMOVED, ABORTED, COMPLETE, STOPPED and ABANDON. The interface combines the state change with the recipe (Batch, UnitProcedure, Operation, or Phase) to determine which recipe step has changed state. 

When `/UBR = true`, the interface uses the Batch Recipe logic as opposed to the STATE CHANGE logic. The interface uses SYSTEM MESSAGE to control the start and end of event frames. Example system messages are BEGIN OF BATCH, END OF BATCH, UNIT PROCEDURE STARTED, and UNIT PROCEDURE ENDED.

Additionally, when UBR=TRUE, the start time for the queried batch events is the ACTIVATETIME instead of the STARTTIME. The end time for the batch events the DEACTIVATETIME instead of ENDTIME.

**Note:** We do not recommend configuring both the UBR and the True Batch Start End (TBSE) command line parameters to TRUE at the same time. These parameters are independent from one another and are best utilized when run in separate configurations.

If both `/TBSE` and `/UBR` are set to TRUE, it is likely that `/TBSE` will overwrite the start and end times of the batch.

### `/uidlist=<list>`

(Optional) Recover specified manufacturing orders, then exit. Specify a comma-separated list of unique IDs for the manufacturing orders to be recovered. This parameter overrides any settings specified for the /rst and /ret recovery switches.

Example: /uidlist=MOKey#1, MOKey#2

### `/uobev` (DeltaV SQL 9.3+ only)

(Optional) Directs the interface to use the original batch event view. By default the interface queries 17 tables to retrieve data for batch-associated events. Note that this view does not provide explicit [Descript], [Pval] and [EU] fields. Instead the [Descript] field combines data from all three fields. This option is provided for backward compatibility.


<!-- Default settings for batch interfaces:

Emerson batch interfaces `/UBR = false`

`/UBR` can be set in the .ini file, on the command line, or by using the PI Event Frames Interface Manager / batch Setup tab.

If `/UBR = true` the interface will use SYSTEM MESSAGE to control the start and end of event frames. Example System Messages are BEGIN OF BATCH, END OF BATCH, UNIT PROCEDURE STARTED, and UNIT PROCEDURE ENDED.

If `/UBR = false` the interface will use STATE CHANGE to control the start and end of event frames. Example State Change messages are RUNNING, REMOVED, ABORTED, COMPLETE, STOPPED, and ABANDON. The interface will combine the state change with the recipe ( Batch, UnitProcedure, Operation, Phase ) to determine which recipe step has changed state.

Provided for backward compatibility with version 1.0.0.0 of the interface.


### `/WEBSRVDISABLED=[true | false]` 

(Optional) If not added it will default to false.

This parameter is only supported in interface PIEMDVBCS and allows the interface to ignore checking or sending requests to the Syncade workflow web services. If connecting to WF 4.9 this parameter must be set to true.

Added in version 4.0.30.

### `/writelink= <AFelementpath>` 

Combine event frames from different interface instances. For an MES controlling one or more BES systems, configure `/writelink` on the MES interface and configure an interface instance for each BES, specifying the same linkage element in the BES `/readlink` setting. The BES interface instances will then create event frame references under the MES event frames that refer to the BES event frames. For Emerson Syncade systems, the AutomationBatchID field must match the batchID of the batch created by the BES.

<<<<<<< HEAD
For a BES interface controlling one or more MES systems, configure /readlink on the MES interface and configure an interface instance for each BES, specifying the same linkage element in the BES /writelink setting. The MES interface will then create event frame references under the BES event frames that refer to the MES event frames. Link templates must also be configured to define which events specify a link. -->

<!-- =======
For a BES interface controlling one or more MES systems, configure `/readlink` on the MES interface and configure an interface instance for each BES, specifying the same linkage element in the BES `/writelink` setting. The MES interface will then create event frame references under the BES event frames that refer to the MES event frames. You must configure Link templates to define which events specify a link.
>>>>>>> 8e2a7c5c24ad8b8033a2f94be546d353ba252ecc -->
