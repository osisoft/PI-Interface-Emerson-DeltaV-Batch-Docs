---
uid: BIF_StartAndStopEvents
---

# Start and stop events

The start and end times set by the interface depend on the type of data source and whether the "Use Batch Recipe" (UBR) option is enabled. The UBR option is provided for backward compatibility with the interface.

<!-- Karl Nyce 02/14/22: Customized for DeltaV -->

For more information on how the interface determines start and end times, refer to the sections below.

## Event Files Data Source
The interface detects start and end events by scanning the [EVENT] field for "State change" events. To determine whether the event is a start or end, the interface scans the [PVALUE] field. To determine the level that started or ended, the interface checks the [RECIPE] field.

### EVT File Default Start and Stop Events
|Recipe Level      |[PVALUE] Start      |[PVALUE] End                        |Remarks                                  |
|------------------|--------------------|------------------------------------|-----------------------------------------|
|Batch             |"CREATED"           |"REMOVED"         |                                                           |
|Unit batch        |"RUNNING"           |"COMPLETE", "STOPPED", or "ABORTED" |Requires equipment acquisition or release event: [EVENT] = "Recipe Arbitration" and [DESCRIPT] = "Resource Acquired by recipe" or "Resource Release by recipe". For unit batch start time, the interface uses the timestamp of the start event or equipment acquisition event, whichever is latest. For end time, it uses the timestamp of the end event or the equipment release event, whichever is earliest. The interface reads the unit name from the [PVALUE] field. |
|Operation         |"RUNNING"           |"COMPLETE", "STOPPED", or "ABORTED" |                                         |
|Phase             |"RUNNING"           |"COMPLETE", "STOPPED", or "ABORTED" |                                         |
|Phase state       |"RUNNING"           |n/a                                 |The state of a phase state ends any preceding phase state. If the interface detects multiple start or end events for the same phase state, it uses the first event. |
|Phase step        |n/a                 |n/a                                 |To enable phase steps, specify the /RAS flag in the INI file or, using PI Event Frames Interface Manager, go to the **Batch Setup** page and enable **Report As Step** and specify start and end text. Phase steps do not create higher-level procedures, unit procedures, and so on, if a parent phase is not found. If no phase step close event is found, the phase step is closed when its parent operation is closed. The interface ignores any zero-duration phase steps. |

## EVT File "Use batch recipe" (UBR) Enable Start and Stop Events
EVT files are used to enable batch start and stop events.

*Batch Recipe Level*

Either of the following enable **Batch** level recipe start events:

[EVENT] = "System Message" and [PVALUE] = "Beginning Of BATCH"

or

[EVENT] = "State Change" and [PVALUE] field = "RUNNING"

Either of these events end a **Batch**:

[EVENT] = "System Message" and [PVALUE] = "End Of BATCH"

or

[EVENT] = "State Change" and [PVALUE] field = "REMOVED", "COMPLETE" or "ABORTED" or "STOPPED" or "ABANDONED"

*Unit Batch Recipe Level*

These events **Start** a **Unit Batch** level recipe:

[EVENT] = "System Message" and [DESCRIPT] field = "Unit Procedure Started"

and 

[EVENT] field = "Recipe Arbitration", [DESCRIPT] field = "Resource Acquired by recipe"

and

[EU] field = "Unit". The [PVALUE] field contains the actual unit name.

The latest timestamp is used as the start time for the Unit Batch.

[EVENT] = "State Change" and [PVALUE] field = "RUNNING"

These events **End** a **Unit Batch** recipe:

[EVENT] = "System Message" and [DESCRIPT] field = "Unit Procedure Finished"

and

[EVENT] field = "Recipe Arbitration", [DESCRIPT] field = "Resource Released by recipe"

and

[EU] field = "Unit". The [PVALUE] field contains the actual unit name.

The earliest timestamp is used as the end time.

Unit Batch end if [EVENT] = "State Change" and [PVALUE] is "REMOVED" or "COMPLETE" or "ABORTED" or "STOPPED" or "ABANDONED"

*Operation Level Recipe*

The following event is the **Start** of an **Operation** level recipe:

[EVENT] = "System Message" and [DESCRIPT] = "Operation Started"

Either of these events End an Operation level recipe:

[EVENT] = "System Message" and [DESCRIPT] field = "Operation Finished"

or

[EVENT] = "State Change" and [PVALUE] field = "REMOVED" and [RECIPE] = "Operation"

The earliest timestamp is used.

*Phase Level Recipe*

The event is the **Start** of a **Phase** level recipe:

[EVENT] = "State Change" and [PVALUE] = "RUNNING"

This event is the **End** of a **Phase** level recipe:

[EVENT] = "State Change" and [PVALUE] = "RUNNING" or "COMPLETE" or "ABORTED"

## SQL Batch Historian
The DeltaV BES stores its batch execution history using Microsoft SQL Server. The interface retrieves history from the DVHisDB database.

### SQL Default Start and Stop Events

|Recipe Level      |[EVENTTYPE]         |[EVENTDESCRIPT] Start               |[EVENTDESCRIPT] End                      |
|------------------|--------------------|------------------------------------|-----------------------------------------|
|Batch             |"State Change"      |CREATED                             |REMOVED                                  |
|Unit batch        |"State Change"      |RUNNING                             |COMPLETE, STOPPED or ABORTED             |
|Operation         |"State Change"      |RUNNING                             |COMPLETE, STOPPED or ABORTED             |
|Phase             |"State Change"      |RUNNING                             |COMPLETE, STOPPED or ABORTED             |
|Phase state       |n/a                 |User-specified text                 |Last phase state in phase: COMPLETE, STOPPED or ABORTED or parent level ends. Preceding phases end when next phase state starts.|

To detect start and end events, the interface queries the following views by default:

* brecipestatechangeview
* batcheventview
* batchequipmentview

By default, batch event start and end times are read from batcheventview. For recipes above phase-level recipes, unit batches require equipment acquisition and release events (unless equipment arbitration events are unavailable). For equipment arbitration events, the interface reads the [AcquireTime] and [ReleaseTime] values from batchequipmentview. For phase states, the start of a state ends any preceding state (in other words, there are no explicit end events for phase states.)

### SQL UBR Start and Stop Events

|Recipe Level      |Database View       |Start time column  |End time column  |Remarks                                  |
|------------------|--------------------|-------------------|-----------------|-----------------------------------------|
|Batch             |batchrecipeview     |[ActivateTime]     |[DeactivateTime] |For "procedure" events                   |
|Unit batch        |batchrecipeview     |[StartTime]        |[EndTime]        |Plus [AcquireTime] and [ReleaseTime] from batchequipmentview|
|Operation         |batchrecipeview     |[StartTime]        |[EndTime]        |                                         |
|Phase             |batchrecipeview     |[StartTime]        |[EndTime]        |                                         |
|Phase state       |brecipestatechangeview or batcheventview|[StartTime]      |[EndTime]|[EventType] field = "State Change" and [EventDescr] field containing the substring <state name>       |

To detect the start and end of levels when the UBR option is enabled, the interface queries the following views:
 
* batchrecipeview
* batchequipmentview
* brecipestatechangeview
* batcheventview

For operation- and phase-level recipes, the interface creates the parent levels (unit batch and batch).

## SQL Query Details
The interface retrieves history from the DVHisDB database, primarily using a query that returns the union of the following tables:
 
* bactivestepchangeevent
* bmaterialchargerequestevent
* bmaterialchargeevent
* bpausestatusevent
* bequipmentselectionevent
* bphaselinkpermissiveevent
* brecipemodechangeevent
* brecipemodecommandevent
* brecipestatechangeevent
* brecipestatecommandevent
* brecipevaluechangeevent
* brecipevaluerequestevent
* breportevent
* btextmessageevent
* bphasebatchrequestevent
* brecipecomment
* unhandledbatchmsg

In addition, the interface retrieves batch-related data from the following views:

|View or Table      |Contents Queried For                                         |
|-------------------|-------------------------------------------------------------|
|batchview          |uniqueid, batchid, start time, end time, product, uniqueid and archived flag with new archived database name for all batches.|
|brecipestatechangeview | State change events, which are used by default to detect start and end of recipe levels. |
|batchrecipeview | Recipe data, equipment linkage, start and end time for each object.|
|batchequipmentview | Equipment arbitration events.|
|batcheventview | Batch-associated data. Queried only if **Use original batch event view** (UOBEV) option is enabled. The [DESCRIPT] column is parsed for [PVAL] and [EU].|
|localevars | Used to convert local start and end times with DST offsets to GMT time and then to UTC seconds.|
 
To detect start and end events, the interface queries the following views by default:
 
* brecipestatechangeview
* batcheventview
* batchequipmentview

Batch event start and end times are read from batcheventview. For recipes above phase-level recipes, unit batches require equipment acquisition and release events (unless equipment arbitration events are unavailable). For equipment arbitration events, the interface reads the [AcquireTime] and [ReleaseTime] values from batchequipmentview. For phase states, the start of a state ends any preceding state (in other words, there are no explicit end events for phase states.)

To detect the start and end of levels when the UBR option is enabled, the interface queries the following views:
 
* batchrecipeview
* batchequipmentview
* brecipestatechangeview
* batcheventview
