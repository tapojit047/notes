# Ingestion:
- Loading data in Druid is called ingestion or indexing. When you ingest data into Druid, Druid reads the data from your source system and stores it in data files called segments. In general, segment files contain a few million rows each.
- Two types of Ingestion possible.
  - Streaming
  - Batch
## Batch Ingestion:
- Definition: Batch ingestion involves loading a large volume of data at once into Druid.
- Use Case: It is suitable for scenarios where you have a static dataset that is periodically updated or refreshed.
- Process: During batch ingestion, data is typically loaded in chunks or batches at specified intervals. The entire dataset is processed and indexed into Druid, and this process is often performed in a scheduled or periodic manner.
- Advantages:
  - Well-suited for historical or static datasets.
  - Can handle large volumes of data in bulk.
## Streaming Ingestion:
- Definition: Streaming ingestion is the process of continuously ingesting real-time data into Druid as it becomes available.
- Use Case: It is ideal for scenarios where data is generated and updated in real-time, and you need to analyze or visualize this data immediately.
- Process: Streaming data is ingested in near real-time or real-time as it flows into the system. This allows for low-latency analytics and quick insights on the most recent data.
- Advantages:
  - Supports real-time analytics and monitoring.
  - Enables low-latency access to the latest data.
- In Druid, the methods for achieving batch and streaming ingestion are as follows:
### Batch Ingestion:
- You can use the Druid Indexing Service to submit batch ingestion tasks. These tasks define how the data should be ingested, transformed, and indexed into Druid.
- Batch ingestion is often used for historical data or for loading large sets of data at scheduled intervals.

### Streaming Ingestion:
- For real-time or streaming data, Druid provides the Tranquility service, which is responsible for ingesting real-time events.
- Tranquility allows you to send real-time events to Druid, and it automatically manages the creation of new segments in the background.