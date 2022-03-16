---
uid: BIF_Interface
---

# [!include[interface](../includes/product-long.md)]

<!-- Customized for DeltaV -->
PI Interface for Emerson DeltaV Batch supports all process components and is designed to be used for DeltaV 10.3 and later systems utilizing the DeltaV OPC A&E Server and the DeltaV Batch Historian. Additionally, you can run the interface against DeltaV 9.3 and DeltaV 8.4 by utilizing different data sources.

A single DeltaV interface instance can collect data from multiple data sources provided all sources are of the same type. This includes DeltaV Batch Historian, Event journal files, DeltaV Alarms and Events server and OPC Alarms and Events server. This interface automatically creates Batches in the PI Batch Database or Event Frames in PI Asset Framework (AF) with corresponding representational asset hierarchies in the Module Database (MDB) or PI AF. Process data can be stored in automatically created PI Tags or in properties attached to Event Frames/Batches based on a flexible template methodology.

