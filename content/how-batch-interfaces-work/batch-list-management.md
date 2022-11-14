---
uid: BIF_batchlistmanagement
---

# Batch List Management

In real time mode, the interface first checks to see if there are batches in the batch list. If there are no batches in the batch list after querying between the query start and end time, the start time remains the same as the current time. 

If there are only closed batches in the list, the interface selects the batch with the most recent start time for the Next Query Start Time from the list of closed batches. If that time falls after the current query start time, then the interface selects the current query start time as the Next Query Start Time.

If there are open batches in the list, the interface selects the batch with the most recent start time for the Next Query Start Time from the list of open batches. If that time falls after the current query start time, then the interface selects the current query start time as the Next Query Start Time.

In history recover mode, the configuration of the [Maximum query time frame (/MAXQTF=)](https://docs.osisoft.com/bundle/pi-interface-emerson-deltav-batch/page/pi-event-frames-interface-manager/time-settings-tab.html) on the Time Setting tab determines the query end time. For example, if the MAXQTF is set to five days, the end time for the queries move forward five days from the query start time. When the interface defines a query start time, the end time moves forward automatically based on the MAXQTF configuration. 
