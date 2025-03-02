# Apache Druid

### Analytics Database:
- An analytics database is a specialized type of database system designed to efficiently store and manage data for the purpose of performing analytics and generating insights. These databases are optimized for complex querying and reporting tasks, allowing organizations to analyze large volumes of data and extract valuable information from it. Here are some key characteristics and features of analytics databases:
  - **Columnar Storage**: Many analytics databases use a columnar storage format rather than row-based storage. This allows for efficient compression and retrieval of data, making queries faster and reducing storage requirements.
  - **Performance**: Analytics databases are designed for high-performance querying and reporting. They can handle complex analytical queries involving aggregations, filtering, and joins on large datasets.
  - **Parallel Processing**: To speed up query processing, analytics databases often leverage parallel processing and distributed computing techniques. They can scale horizontally by adding more nodes to a cluster.
  - **Compression**: Data compression techniques are employed to reduce storage space and improve query performance. Columnar databases, in particular, benefit from this as they can skip reading irrelevant data during queries.
  - **Indexing**: Analytics databases may use indexing structures like bitmap indexes, B-tree indexes, or other specialized indexes to accelerate query execution.
  - **Support for SQL**: Most analytics databases provide SQL-like query languages, making them accessible to analysts and data scientists who are familiar with SQL.
  - **Time-Series Data Support**: Many analytics databases excel at handling time-series data, which is common in applications like log analysis, monitoring, and IoT (Internet of Things) data.
  - Real-Time Data Ingestion**: Some analytics databases support real-time data ingestion, allowing organizations to analyze streaming data as it arrives.
  - **Integration**: They often integrate with popular business intelligence (BI) tools and data visualization platforms, making it easier to create dashboards and reports.
  - **Scalability**: Analytics databases can scale horizontally to accommodate growing data volumes and query loads.
  - **Data Transformation**: Some analytics databases offer built-in ETL (Extract, Transform, Load) capabilities to clean and preprocess data before analysis.
  - **Security**: Data security features are essential to protect sensitive information in the database. This includes role-based access control and encryption.
  - **Data Governance**: Analytics databases may support data governance features such as auditing, data lineage tracking, and data versioning.
- Common use cases for analytics databases include business intelligence, data warehousing, ad-hoc reporting, customer analytics, fraud detection, and more. Popular examples of analytics databases include Amazon Redshift, Google BigQuery, Snowflake, Apache Druid, and more. The choice of an analytics database depends on the specific needs and requirements of an organization's analytics and reporting tasks.

### OLAP (Online Analytical Processing) :
#### Dimesions and Measures:
  - [Video](https://www.youtube.com/watch?v=qkJOace9FZg)
  - **Dimensions**:
    - Definition: Definition: Dimensions are the categorical or qualitative attributes by which data is categorized, organized, or sliced. They represent the various ways you can view and group data. Dimensions provide context and help break down data into meaningful categories.
    - Examples:
      - Time: Time-related dimensions like date, month, quarter, and year.
      - Geography: Geographical dimensions like country, region, city, or postal code.
      - Product: Dimensions related to products or services, such as product category, brand, or SKU.
      - Customer: Dimensions related to customers, like customer ID, name, or demographic information.
      - Employee: Dimensions related to employees, such as employee ID, department, or job title.
    - Use: Dimensions are typically used for grouping and categorizing data. When you want to break down or filter data by specific attributes to gain insights, you use dimensions. For example, you might want to analyze sales by region (geographical dimension) or track website traffic by date (time dimension).

  - **Metrics**:
    - Definition: Metrics, also known as measures or key performance indicators (KPIs), are the quantitative or numerical values that represent the data you're analyzing. Metrics are the values you want to measure, track, or analyze to gain insights into your business or operations.
    - Examples:
      - Revenue: The total sales revenue generated by a company.
      - Profit: The net income after deducting expenses from revenue.
      - Website Traffic: The number of visitors to a website.
      - Customer Satisfaction Score (CSAT): A numerical rating reflecting customer satisfaction.
      - Inventory Level: The quantity of products in stock.
    - Use: Metrics are used to quantify and analyze data. They provide the numerical basis for understanding the performance or status of a business or system. Metrics can be aggregated, compared, and visualized to make data-driven decisions. For instance, you might want to analyze revenue trends over time (using time as a dimension) or compare the performance of different product categories (using product as a dimension).
-  In data analysis and reporting, dimensions and metrics work together. You often analyze metrics with respect to one or more dimensions to answer questions and derive insights. For example, you might analyze revenue (metric) by region (dimension) to determine which geographic areas are the most profitable. Using dimensions and metrics effectively helps make data more meaningful and actionable in various domains, from business intelligence to marketing analytics.

  - **Hierarchy**:
    - A hierarchy refers to an organized structure of levels or categories that represent a relationship between different elements of data. Hierarchies are used to organize and navigate data in a way that reflects their natural or logical order. Hierarchies are especially important in OLAP (Online Analytical Processing) systems and data modeling. Here are some key points about hierarchies:
      - Levels: Hierarchies consist of different levels, each representing a specific degree of granularity or detail. The levels are organized from higher (more general) to lower (more specific) levels. For example, in a time hierarchy, you might have levels like Year, Quarter, Month, and Day, with Year being the highest level of granularity and Day being the lowest.
      - Parent-Child Relationships: Hierarchies define parent-child relationships between levels. Each level has one or more members, and these members can be related to members at other levels. For instance, a Year can have multiple Quarters, and each Quarter can have multiple Months.
      - Drill-Down and Roll-Up: One of the primary benefits of hierarchies is the ability to perform drill-down and roll-up operations. Drill-down allows you to move from a higher level of granularity to a lower one, gaining more detail. Roll-up, on the other hand, is the reverse process, where you aggregate data from lower levels to higher levels.
      - Dimension Hierarchies: In OLAP systems, hierarchies are often associated with dimensions. For example, in a product dimension, you might have a hierarchy that includes levels like Product Category, Subcategory, and Product Name. This hierarchy allows users to navigate product data from broad categories to specific products.
      - User-Friendly Navigation: Hierarchies make data more user-friendly and intuitive. Users can explore data at the level of detail that suits their needs and easily move between different levels to gain insights. This is particularly useful in business intelligence and reporting tools.
      - Examples of Hierarchies:
        - Time Hierarchy: Year > Quarter > Month > Day
        - Geographical Hierarchy: Continent > Country > Region > City
        - Product Hierarchy: Category > Subcategory > Product
        - Organizational Hierarchy: Company > Department > Team > Employee
      - Data Modeling: When designing databases or data warehouses, hierarchies are often modeled to represent the relationships between entities. For example, an organizational hierarchy can be used to model the reporting structure within a company.
      - Visualization: Hierarchies are commonly used in data visualization tools to create hierarchical charts, such as treemaps, sunbursts, or drill-down bar charts, that allow users to interactively explore data.
    - In summary, hierarchies provide a structured way to organize and navigate data, allowing users to move between different levels of granularity and gain insights from their data. They are an essential concept in data modeling, OLAP systems, and data analysis, enabling more intuitive and effective exploration of complex datasets.

### Data Warehouse:
- [Video](https://www.youtube.com/watch?v=B3gJT3t8g4Q)
- A data warehouse is a centralized repository of integrated and carefully organized data that is designed to support business intelligence (BI), reporting, and data analysis. It serves as a critical component in the decision-making process of organizations by providing a unified and historical view of data from various sources. Here are key characteristics and components of a data warehouse:
  - Data Integration: Data warehouses gather data from different source systems, such as operational databases, external sources, spreadsheets, and more. The data integration process involves extracting, transforming, and loading (ETL) data into the warehouse to ensure consistency and quality.
  - Structured Data: Data in a data warehouse is typically structured and organized into tables, rows, and columns. This structured format enables efficient querying and reporting.
  - Historical Data: Data warehouses maintain historical data, allowing users to analyze trends and patterns over time. This historical perspective is essential for making informed business decisions.
  - Subject-Oriented: Data warehouses are organized around specific subject areas or business domains, such as sales, finance, marketing, or inventory. Each subject area is known as a data mart.
  - Data Transformation: Data in a warehouse often undergoes transformation processes to clean, standardize, and aggregate it. This transformation ensures data consistency and makes it suitable for analytical purposes.
  - Dimensional Modeling: Dimensional modeling is a common technique used in data warehousing. It involves designing data models that include facts (numeric data) and dimensions (attributes by which data is analyzed) to facilitate easy querying and reporting.
  - Query Performance Optimization: Data warehouses are optimized for querying and reporting. They employ techniques like indexing, partitioning, and materialized views to improve query performance.
  - Data Security: Data warehouses implement security measures to protect sensitive data. Access control and encryption are often used to ensure data privacy and compliance with regulations.
  - Data Visualization and Reporting: Data from the warehouse can be used to create visualizations, dashboards, and reports that help users gain insights and make data-driven decisions.
  - Scalability and Redundancy: Modern data warehouses are scalable and may be distributed across multiple servers or the cloud to handle large volumes of data. They also incorporate redundancy and failover mechanisms for data availability.
  - Business Intelligence Tools: Data warehouses are often paired with business intelligence tools like Tableau, Power BI, or QlikView, which provide user-friendly interfaces for data exploration and analysis.
  - Examples: Popular data warehousing solutions include Amazon Redshift, Google BigQuery, Snowflake, Microsoft Azure SQL Data Warehouse, and on-premises solutions like Oracle Exadata and IBM Db2 Warehouse.
- Data warehouses play a crucial role in helping organizations consolidate data from disparate sources, gain a comprehensive view of their operations, and make data-driven decisions. They are particularly valuable for complex analytical queries and reporting tasks that require historical data and involve large datasets.

### OLAP:
- [Video](https://www.youtube.com/watch?v=2ryG3Jy6eIY)
- [IBM Blog](https://www.ibm.com/topics/olap)
- [Blag](https://www.techtarget.com/searchdatamanagement/definition/OLAP)
- OLAP stands for Online Analytical Processing, and it is a computer-based approach to extracting useful and valuable information from large volumes of data. OLAP systems are designed to help users interactively analyze multidimensional data stored in data warehouses or data marts. Here are some key aspects of OLAP:
  - Multidimensional Data Model: OLAP systems organize data in a multidimensional model. In this model, data is stored in a way that allows users to explore it from various perspectives, such as time, geography, products, and more. It enables users to analyze data across multiple dimensions simultaneously, providing a rich and flexible way to view information.
  - Cubes: Data in OLAP is typically represented as data cubes. A data cube is a multidimensional representation of data that consists of measures (numeric data) and dimensions (attributes by which data can be sliced and diced). Users can drill down into or roll up data within these cubes to explore different levels of detail.
  - Aggregation: OLAP systems provide aggregation capabilities, allowing users to summarize and aggregate data at different levels of granularity. This can include totals, averages, and other calculations. Aggregation helps users gain insights into overall trends and patterns.
  - Fast Query Performance: OLAP databases are optimized for query performance. They use techniques like pre-aggregation and indexing to ensure that users can interact with and retrieve data quickly, even when dealing with large datasets.
  - Interactive Analysis: One of the primary goals of OLAP is to support interactive analysis. Users can explore data, slice and dice it, and drill down to get more detailed information. This interactivity is essential for business intelligence and decision-making processes.
  - Types of OLAP: There are different types of OLAP systems, including MOLAP (Multidimensional OLAP), ROLAP (Relational OLAP), and HOLAP (Hybrid OLAP). MOLAP stores data in multidimensional cubes, ROLAP uses relational databases to store data, and HOLAP combines elements of both approaches.
  - Data Warehouses: OLAP systems often rely on data warehouses, which are large repositories of data gathered from various sources. Data warehouses are designed to support reporting and analysis, and they often feed data into OLAP systems.
- OLAP is widely used in business intelligence and data analysis applications to help organizations make informed decisions, identify trends, and discover insights from their data. It enables users to explore data in a way that is intuitive and conducive to decision-making processes, making it a valuable tool in the world of data analytics and reporting.

### Slice-and-Dice in OLAP:
- "Slicing" and "dicing" are fundamental operations in OLAP (Online Analytical Processing) that allow users to interactively explore and analyze multidimensional data cubes to gain insights. These operations help users examine data from different perspectives by selecting specific subsets of data or by reorganizing dimensions within the cube. Here's what slicing and dicing mean in OLAP:
  - **Slicing**:
    - Definition: Slicing involves selecting a single dimension from a multidimensional data cube and viewing a two-dimensional "slice" of data from that cube. This operation effectively reduces the cube's dimensions by one, focusing on a particular attribute of interest.
    - Example: Suppose you have a sales data cube with dimensions for Time (Year, Quarter, Month), Product (Category, Subcategory), and Region (Country, State). If you slice the cube by selecting the "Year" dimension and specifying "2023," you would be viewing a slice of data for the year 2023, effectively eliminating the time dimension's variability.
    - Purpose: Slicing allows you to isolate data along one dimension to analyze it in detail, explore trends over a specific period, or compare different values within that dimension.
  - Dicing:
    - Definition: Dicing involves selecting specific values from two or more dimensions of a multidimensional data cube to create a subcube with reduced dimensions. This operation provides a more focused view of data by narrowing down the possibilities within those dimensions.
    - Example: Using the same sales data cube, if you decide to dice the cube by selecting "Product Category" as "Electronics" and "Region" as "United States," you would create a subcube that contains sales data for Electronics products in the United States.
    - Purpose: Dicing allows you to zoom in on particular combinations of dimension values, making it useful for conducting detailed analyses, comparisons, or drilling down into specific subsets of data.
- In summary, slicing and dicing are OLAP operations that help users navigate multidimensional data cubes to extract valuable insights. Slicing involves selecting a single dimension to view a cross-section of data, while dicing involves selecting specific values from multiple dimensions to create a subcube of interest. These operations are essential for interactive data exploration and analysis in OLAP systems, providing flexibility and the ability to view data from different angles.
- In simple words Slicing and dicing in OLAP are like ways of looking at and cutting up a big cake made of data.
  - **Slicing** is like cutting a thin piece of cake from top to bottom. It's when you want to see just one part of the cake, like only the chocolate part or only the strawberry part. In data terms, it's when you pick just one category or one year to look at and ignore the rest.
  - **Dicing** is like cutting a small square piece out of the cake. It's when you want to see a specific combination, like chocolate cake with strawberries on top. In data terms, it's when you pick specific things from different categories, like "chocolate cake" from the desserts category and "strawberries" from the toppings category.
- So, slicing is about looking at one part, while dicing is about looking at a special mix of parts from your data cake. These actions help you understand your data better by focusing on what's most important for your analysis.


### Columnar Storage: 
- [Video](https://www.youtube.com/watch?v=8KGVFB3kVHQ)
- Columnar storage is a database storage format that organizes data in columns rather than rows. In a traditional row-based storage system, data for each row is stored together in a contiguous block, while in a columnar storage system, all values for a single column are stored together in a contiguous block. This design choice offers several advantages, especially for analytics and reporting workloads. 
- Here are some key characteristics and advantages of columnar storage formats:
  - Improved Query Performance: Columnar storage is particularly well-suited for analytical and reporting workloads because it allows for more efficient data retrieval. When you only need specific columns for a query, you can skip reading the entire row, which can significantly reduce I/O operations and improve query performance.
  - Compression: Columns with similar data types tend to have similar values, which makes them highly compressible. This compression reduces storage space requirements and can lead to faster query execution due to reduced I/O.
  - Predicate Pushdown: Many modern database systems and query engines can take advantage of columnar storage to perform predicate pushdown. This means that the database can filter out unnecessary data before it is even read from storage, further improving query performance.
  - Aggregation Efficiency: Aggregation operations, such as sum, count, or average, can be performed more efficiently on columnar data because you're working with contiguous data of the same type.
  - Schema Evolution: Columnar storage formats often support schema evolution, allowing you to add or remove columns with relative ease. This flexibility can be helpful in evolving data schemas over time.

### Analytics Application:
- An analytics application, also known as a data analytics application, is software or a computer program designed to perform data analysis, process large volumes of data, and provide insights, reports, and visualizations to help users make informed decisions. These applications are used to extract valuable information and patterns from data, enabling organizations to optimize their operations, identify trends, make predictions, and gain a competitive edge.

### Apache Druid:
- [DOCS](https://druid.apache.org/docs/latest/design/)
- Apache Druid, formerly known as Druid, is an open-source, real-time analytics database designed to handle large volumes of data and provide fast query performance for interactive and exploratory analytics. It was originally developed by Metamarkets (now part of Snap Inc.) and later donated to the Apache Software Foundation, where it became an Apache top-level project.
- Key features of Apache Druid include:
  - Real-time Ingestion: Druid is designed to ingest data in real-time, making it suitable for applications that require up-to-the-minute analytics and reporting. It can handle streaming data sources like Apache Kafka, AWS Kinesis, and more.
  - Columnar Storage: Druid uses a columnar storage format, which optimizes query performance by only reading the necessary columns for a given query. This reduces I/O operations and speeds up data retrieval.
  - Scalability: Druid is horizontally scalable, which means you can add more nodes to your cluster as your data volume and query load grow. This makes it suitable for handling large datasets and high query concurrency.
  - Interactive Querying: It provides sub-second query response times, making it ideal for interactive data exploration and dashboards. Users can perform ad-hoc queries and drill-down analysis on their data.
  - Time-Series Data Support: Druid is particularly well-suited for time-series data, making it a popular choice for monitoring, log analysis, and other applications where timestamped data is essential.
  - Extensible Architecture: Druid's modular architecture allows for extensions and customizations to meet specific use cases. You can plug in different components like indexing modules, storage formats, and query engines.
  - Schema-less Ingestion: Druid allows for schema-less data ingestion, making it flexible and accommodating for various data formats and structures.
  - Built-in Aggregations: It supports various aggregation functions, which are essential for summarizing and analyzing data.
  - Integration: Druid can be integrated with popular data visualization and business intelligence tools, making it easy to create interactive dashboards and reports.
  - SQL-like Query Language: Druid provides a SQL-like query language that makes it accessible to users who are familiar with SQL.
- Apache Druid finds applications in a wide range of use cases, including monitoring and observability, ad-hoc analytics, business intelligence, fraud detection, and more. It is particularly popular in industries like e-commerce, digital advertising, and online gaming, where real-time analytics are crucial for decision-making.

### Configurations:
#### Deployment:
- Single machine deployment and clustered deployment refer to two distinct ways of setting up and configuring a software application or system like Apache Druid, depending on your use case and requirements. Here are the key differences between the two deployment approaches:
  - **Single Machine Deployment**:
    - Scope: In a single machine deployment, the entire application or system runs on a single physical or virtual machine. This configuration is suitable for small-scale or development environments where data volumes and processing demands are relatively low.
    - Resource Limitations: Single machine deployments are constrained by the resources (CPU, memory, storage) of the host machine. As a result, they have limited scalability and processing capacity.
    - Simplicity: Setting up a single machine deployment is typically simpler and requires less configuration. It's often used for testing, development, and learning purposes.
    - Use Cases: Single machine deployments are suitable for learning, prototyping, and small-scale data analysis or processing tasks. They are not well-suited for handling large volumes of data or high-throughput workloads.

- **Clustered Deployment:**
  - Scope: In a clustered deployment, the application or system is distributed across multiple machines (nodes) that work together as a cluster. Each node in the cluster can perform various tasks, and data is distributed and processed across nodes.
  - Scalability: Clustered deployments are designed for scalability and can handle large volumes of data and high-throughput workloads. You can add or remove nodes from the cluster to adjust its capacity.
  - High Availability: Clustering provides high availability and fault tolerance. If one node in the cluster fails, other nodes can take over its responsibilities, ensuring continuous operation.
  - Complexity: Clustered deployments are more complex to set up and maintain compared to single machine deployments. They require configuration for distributed data storage, load balancing, and coordination between nodes.
  - Use Cases: Clustered deployments are suitable for production environments where scalability, fault tolerance, and high availability are crucial. They are commonly used in big data processing, analytics, and web applications with heavy traffic.
- In summary, the main difference between single machine and clustered deployments is the scale and complexity of the deployment. Single machine deployments are simple and suitable for small-scale or learning purposes, while clustered deployments are designed for scalability, high availability, and handling large-scale data and workloads in production environments. The choice between the two depends on your specific use case and performance requirements.

### Architecture of a simple Druid Cluster:
- **Master Server**: A Master server to host the Coordinator and Overlord processes.
  - **_Coordinator_**: The Druid Coordinator process is primarily responsible for segment management and distribution. More specifically, the Druid Coordinator process communicates to Historical processes to load or drop segments based on configurations. The Druid Coordinator is responsible for loading new segments, dropping outdated segments, ensuring that segments are "replicated" (that is, loaded on multiple different Historical nodes) proper (configured) number of times, and moving ("balancing") segments between Historical nodes to keep the latter evenly loaded.
  - **_Overlord_**: The Overlord process is responsible for accepting tasks, coordinating task distribution, creating locks around tasks, and returning statuses to callers.
- **Data Servers** (Historical and MiddleManager): Two scalable, fault-tolerant Data servers running Historical and MiddleManager processes.
  - **_Historical_**: 
    - Each Historical process copies or "pulls" segment files from Deep Storage to local disk in an area called the segment cache.
    - The Coordinator controls the assignment of segments to Historicals and the balance of segments between Historicals. Historical processes do not communicate directly with each other, nor do they communicate directly with the Coordinator. Instead, the Coordinator creates ephemeral entries in Zookeeper in a load queue path. Each Historical process maintains a connection to Zookeeper, watching those paths for segment information.
  - **_MiddleManager_**: The MiddleManager process is a worker process that executes submitted tasks. Middle Managers forward tasks to Peons that run in separate JVMs. The reason we have separate JVMs for tasks is for resource and log isolation. Each Peon is capable of running only one task at a time, however, a MiddleManager may have multiple Peons.
- **Query Server**: A query server, hosting the Druid Broker and Router processes
  - _**Broker**_: The Broker is the process to route queries to if you want to run a distributed cluster. It understands the metadata published to ZooKeeper about what segments exist on what processes and routes queries such that they hit the right processes. This process also merges the result sets from all of the individual processes together. On start up, Historical processes announce themselves and the segments they are serving in Zookeeper.
  - _**Router**_: The Router is responsible for routing queries to the appropriate components, including the Druid Broker. In addition to query routing, the Router also runs the web console, a management UI.
- **Deep Storage**: "Deep storage" refers to a storage system or repository where the actual data or data segments used for analysis and querying are stored.
- This architecture is a simplified representation of a Druid cluster suitable for many use cases. Druid clusters can be scaled horizontally by adding more historical nodes or real-time nodes to handle larger data volumes and query loads. Additionally, Druid can be integrated with other tools and services for data ingestion and integration, such as Apache Kafka for real-time data streaming and Apache Hive for SQL query capabilities.
- In production, we recommend deploying multiple Master servers and multiple Query servers in a fault-tolerant configuration based on your specific fault-tolerance needs.

- ** Historical Vs MiddleManager Vs Deep Storage_**:
- In the context of Apache Druid, Historical and MiddleManager are two different types of server processes that play distinct roles in the system, while deep storage is a storage component that is separate from these processes. Let's explore the differences:
  - Historical:
    - Role: Historical processes in Druid are responsible for serving historical data segments to query processes (like brokers). They are essentially responsible for providing access to historical data for querying and analysis.
    - Data Segments: Historical processes store and manage the actual data segments that have been ingested into Druid. These segments contain pre-aggregated data that is ready for querying.
    - Data Retention: Historical processes can be configured to retain and serve historical data for a specified period. They can store data segments on local storage or access data from deep storage when needed.
    - Scalability: Historical processes can be added or removed from the Druid cluster to scale storage capacity and query throughput as needed.
  - MiddleManager:
    - Role: MiddleManager processes are responsible for coordinating the ingestion of data into Druid. They manage the tasks related to data ingestion, including data ingestion, indexing, and segment creation.
    - Data Ingestion: MiddleManagers work with the indexing service to process incoming data and convert it into Druid segments. They split and distribute tasks among the available resources for parallel processing.
    - Real-Time Ingestion: MiddleManager plays a critical role in real-time data ingestion, ensuring that newly arriving data is ingested, processed, and made available for querying in near-real-time.
    - Scalability: MiddleManagers can be added or removed from the cluster to scale the ingestion capacity of Druid.
  - Deep Storage:
    - Role: Deep storage is a separate storage component used to store the actual data segments generated by Druid. It serves as a durable and scalable storage repository for historical and real-time data segments.
    - Data Durability: Deep storage is designed for data durability and long-term data retention. It ensures that data remains available even if servers are restarted or replaced.
    - Storage Solutions: Deep storage can be implemented using various storage solutions, including cloud-based object storage (e.g., Amazon S3, Azure Blob Storage), distributed file systems (e.g., HDFS), or network-attached storage (e.g., NFS).
    - Data Separation: Deep storage decouples the storage of data from the query and ingestion processes. This separation allows data to be accessed and queried independently of the servers responsible for data ingestion and serving.
  - In summary, Historical and MiddleManager processes in Druid have specific roles related to data storage, retrieval, and data ingestion, while deep storage is a separate storage layer responsible for durable, scalable, and long-term storage of data segments. These components work together to enable Druid to efficiently ingest, store, and serve data for analytical queries.


### ZooKeeper:
- ZooKeeper is an open-source, highly reliable, distributed coordination service. It is often used in distributed systems to manage and coordinate various aspects of the system, such as configuration management, distributed synchronization, and naming services. ZooKeeper provides a centralized and consistent way for distributed applications to synchronize and share information in a distributed environment.

### druid-kubernetes-extensions:
- Apache Druid Extension to enable using Kubernetes API Server for node discovery and leader election. This extension allows Druid cluster deployment on Kubernetes without Zookeeper. It allows running multiple Druid clusters within same Kubernetes Cluster, See clusterIdentifier config below.
- To use this extension please make sure to include `druid-kubernetes-extensions` in the extensions load list.
- This extension works together with HTTP based segment and task management in Druid. Consequently, following configurations must be set on all Druid nodes / `common.runtime.properties`.
  - `druid.zk.service.enabled=false` 
  - `druid.serverview.type=http`
  - `druid.coordinator.loadqueuepeon.type=http`
  - `druid.indexer.runner.type=httpRemote`
  - `druid.discovery.type=k8s`
- For Node Discovery, Each Druid process running inside a pod "announces" itself by adding few "labels" and "annotations" in the pod spec. Druid process needs to be aware of pod name and namespace which it reads from environment variables `POD_NAME` and `POD_NAMESPACE`. These variable names can be changed, see configuration below. But in the end, each pod needs to have self pod name and namespace added as environment variables.

#### Gotchas:
- Label/Annotation path in each pod spec MUST EXIST, which is easily satisfied if there is at least one label/annotation in the pod spec already. This limitation may be removed in future.
- All Druid Pods belonging to one Druid cluster must be inside same kubernetes namespace.
- All Druid Pods need permissions to be able to add labels to self-pod, List and Watch other Pods, create and read ConfigMap for leader election. Assuming, "default" service account is used by Druid pods, you might need to add following or something similar Kubernetes Role and Role Binding.
```YAML
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: druid-cluster
rules:
- apiGroups:
  - ""
  resources:
  - pods
  - configmaps
  verbs:
  - '*'
---
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: druid-cluster
subjects:
- kind: ServiceAccount
  name: default
roleRef:
  kind: Role
  name: druid-cluster
  apiGroup: rbac.authorization.k8s.io
```