---
uid: BIF_StartAndStopEvents
---

# Start and stop events

<!-- Topic requires customization for specific interface -->

The start and end times set by the interface depend on the type of data source and whether the "Use Batch Recipe" (UBR) option is enabled. The UBR option is provided for backward compatibility with the interface.

For each level, **Syncade** records the start time in the [StartUtcDateTime] timestamp and end time in the [EndUtcDateTime] timestamp of the object in which the event is recorded. For phase- and operation-level recipes, the interface creates parent procedures and unit procedures, using the start and end times of the operation or phase to start and end the parent levels. **Syncade** does not provide phase state or phase step data. The batch ID comes from the batch object's [OrderNumber] property, and the batch recipe type is provided for each object by the data source. 