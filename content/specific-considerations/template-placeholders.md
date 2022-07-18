---
uid: BIF_TemplatePlaceholders
---


# Template placeholders

<!-- Customized for DeltaV -->

The following sections list placeholders provided by the interface for defining template settings.

## DeltaV Batch Historian

| Placeholder | Relationship to Source Column | Source Column | View or Union of tables [^1] |
| ----------- | ----------------------------- | ------------- | ------------------------ |
| [AREA] | equivalent to | area | batcheventview |
| [BATCHID] | equivalent to | batchID | batcheventview |
| [COMMENT] | Paragraph | userComment | Union of tables |
| [DESCRIPT] | equivalent to | eventdescr | batcheventview |
| [EU] | Paragraph | engUnit | Union of tables |
| [EVENT] or [PARAMETER] | equivalent to | eventType | batcheventview |
| [OPERATION] | determined from equivalent to | action | batcheventview |
| [PHASE] | determined from equivalent to | action | batcheventview |
| [PHASEMODULE] | equivalent to | phasemodule | batcheventview |
| [PROCEDURE] | determined from equivalent to | action | batcheventview |
| [PROCESSCELL] | equivalent to | processcell | batcheventview |
| [PVAL] or [VALUE] |  | Paragraph | Union of tables[^2] | 
| [UNIQUEID] | equivalent to | uniqueid | batcheventview |
| [UNIT] | equivalent to | unit | batcheventview |
| [UNITPROCEDURE] | determined from equivalent to | action | batcheventview |
| [USERID] or [USER] | equivalent to | userName | batcheventview |

[^1]: Named view or union of tables as described in the topic: Emerson start and stop events
[^2]: Value appropriate to each table in the union of tables, for example: the value column of the BReportEvent table.

For the **VALUE** setting and for **NAME** in property templates, the additional placeholders [TAG] and [TIME] are supported.

## DeltaV Event Chronicle (Alarms & Events Historian) Placeholders

* [AREA]
* [ATTRIBUTE]
* [CATEGORY]
* [DESC1]
* [DESC2]
* [EVENT]
* [LEVEL]
* [MODULE]
* [MODULEDESC]
* [NODE]
* [STATE]
* [TIME]
* [UNIT] (If [MODULEDESC] is "Unit Module", the [UNIT] placeholder contains the module name. Otherwise it contains the unit name.)
