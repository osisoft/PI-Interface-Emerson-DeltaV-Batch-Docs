---
uid: BIF_DataSources
---

# Data sources

<!-- Customized for DeltaV -->

Emerson **Syncade** batch interface collects data historically from **Syncade** web services and real-time data from the Microsoft Message Queue (MSMQ).

To configure the interface to collect historical data from a **Syncade** web service, specify the hostname of the **Syncade** web service host on the **Source** tab of the PI Event Frame Interface Configuration Manager as a URL. For example:

`https://My**Syncade**Host.int:8081/emrWF/WebService/OrdersInterface.asmx`
    
**Note:** You only need to specify the complete URL.

To configure the interface to collect real-time data from the Microsoft Message Queue, ensure that the **Syncade** system is configured to write data to a message queue on the interface machine and, on the Source tab of the PI Event Frame Interface Configuration Manager, select that message queue.

![web service source](../images/web-service-source.png)

```text
SOURCE[1].msmqpath=localhost\private$\QueueForOSIjshearouse Source[1].websrvpath=https://localhost:8081/emrWF/WebService/OrdersInterface.asmx
```
