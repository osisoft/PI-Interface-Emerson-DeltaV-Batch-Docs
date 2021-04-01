---
UID: EmersonSyncadedatasources
---

# Emerson Syncade data sources

The Emerson Syncade batch interface can collect from the same data sources as the Emerson DeltaV batch interface (EVT files and SQL Server). In addition, the interface can collect historical data from Syncade web services and real-time data from the Microsoft Message Queue (MSMQ).
To configure the interface to collect historical data from a Syncade web service, specify the hostname of the Syncade web service host on the Source tab of the PI Event Frame Interface Configuration Manager as a URL.


For example: MySyncadeHost.int.
	
You only need to specify the hostname and not the hostname and protocol combination. 