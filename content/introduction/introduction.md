---
uid: introduction
---

# Introduction to [!include[interface](../includes/product-long.md)] [!include[interface](../includes/product-version.md)]

Emerson DeltaV is is a plant operations digital automation system that uses batch events to manage production processes. 

PI Interface for Emerson DeltaV Batch is a scan-based interface that collects batch processing events from the DeltaV System, collecting batch events in real-time through the DeltaV OPC Alarm & Events Server (A&E Server). The interface stores them in PI Batch Database, and collects associated batch data to PI Tags and PI Batch properties. It populates the PI Batch Database and PIModule Database. 

Associated batch data, such as operator comments, report parameters, and recipe parameters, are retrieved by querying the DeltaV Batch Historian during each interface scan. If you lose the connection to the DeltaV OPC A&E Server, the interface retrieves batch data and associated batch data from the DeltaV Batch Historian during each interface scan. 

The interface automatically tries to re-establish the connection to the DeltaV OPC A&E Server; once the connection has been re-established, the interface returns to collecting batch data in real-time through the DeltaV OPC A&E Server.

This interface is primarily designed to be used for DeltaV 10.3 and later systems utilizing the DeltaV OPC A&E Server and the DeltaV Batch Historian; however, it can run against earlier systems utilizing different data sources.  

* For DeltaV 9.3 systems, this interface can utilize the DeltaV Batch Historian or DeltaV event files as the primary data source.  
* For DeltaV 8.4 systems, this interface can only use DeltaV event files as the primary data source.

**NOTE:**  The use of DeltaV event files as a public interface for the DeltaV System is not recommended by Emerson. 

The flow of data in the interface is unidirectional. Data can only be read from the specified data source and written to the PI Server. This interface can read data from multiple batch data sources simultaneously. By design, the interface does not edit or delete source data. 

In addition to batch data, the interface can populate the PI Point Database. PI Point creation, commonly known as tag creation and event population, is controlled by using tag templates. All modules, tags, tag aliases, and health tags are automatically created on the PI server. The Interface does not use the PI API Buffering Service because batch and tag data is already buffered by the source historian databases. To maximize performance, the interface writes events to PI tags in bulk; that is, it writes all events per interface scan.
