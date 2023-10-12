# Druid-K8S-extension:

## ZooKeeper Use Case:
- **State Synchronization**:
  - Segment Assignment (Load/Dop) to Historical Nodes
  - Segment Announcements by DataNodes
  - Task Assignment
  - Task Runtime State and Status
- **Other**:
  - Node/Service Discovery
  - Leader Election

##  Druid: State Synchronization with ZooKeeper:
![Screenshot from 2023-10-12 17-52-37.png](..%2F..%2Fimages%2FScreenshot%20from%202023-10-12%2017-52-37.png)

![Screenshot from 2023-10-12 17-53-14.png](..%2F..%2Fimages%2FScreenshot%20from%202023-10-12%2017-53-14.png)

##  Druid: State Synchronization without ZooKeeper: (druid-k8s-extension)
**HTTP Long Polling:**
- In general, on Http request, server tries to respond immediately.
- In Long polling, Server "holds" the request till it has updates or a timeout occurs.
- In this approach, Druid components communicate with each other using HTTP. Unlike standard HTTP requests where the server attempts to respond immediately, with long polling, the server "holds" the request until it has updates to send or a timeout occurs.

![Screenshot from 2023-10-12 17-55-14.png](..%2F..%2Fimages%2FScreenshot%20from%202023-10-12%2017-55-14.png)

![Screenshot from 2023-10-12 17-53-40.png](..%2F..%2Fimages%2FScreenshot%20from%202023-10-12%2017-53-40.png)

- Broker will always have a request open to DataNode. As soon as any update occurs Data Node Responds to the request. And after that the broker sends another req immediately.
- **Asynchronous Request/Response**: This approach allows asynchronous request/response patterns in Druid. Brokers maintain open requests to data nodes, and data nodes respond when updates occur. The broker then immediately sends another request to check for further updates.

## Node/Service Discovery:
Druid: Pluggable Discovery and Leadership Interfaces:
- DruidNodeAnnouncer
- DruidNodeDiscoveryProvider
- DruidLeaderSelector

- In Druid, the concept of "Pluggable Discovery and Leadership Interfaces" is used to enable the discovery of nodes or services within a Druid cluster and to select leaders for various roles. These interfaces are designed to be extensible, allowing developers to implement their own plugins using different systems, such as ZooKeeper, etcd, or Kubernetes (K8S). Here's how these interfaces work within the context of Druid's node and service discovery:
  - **DruidNodeAnnouncer**: This interface is responsible for announcing the presence of a Druid node or service. When a Druid process starts up, it uses this interface to update its own Kubernetes pod definition with certain labels and annotations that indicate its role and identity within the cluster. These labels and annotations are used for discovery and leadership purposes.
  - **DruidNodeDiscoveryProvider**: This interface is used to discover other nodes or services within the Druid cluster. It allows Druid processes to query Kubernetes resources to identify nodes with specific roles. By implementing this interface using Kubernetes APIs, Druid can effectively discover other Druid nodes or services running within the same Kubernetes cluster.
  - **DruidLeaderSelector**: This interface is responsible for selecting leaders for various roles within the Druid cluster. Leadership is crucial for tasks like coordination, decision-making, and distribution of work. By implementing this interface using Kubernetes APIs, Druid can perform leader elections within the Kubernetes environment.

- **Node/Service Announcement with K8S**:
- Druid process, on startup, updates self pod def with following:
- labels:
```YAML
druidDiscoveryAnnouncement-<nodeRole.getJsonName()> = true
druidDiscoveryAnnouncement-id-hash = hashEncodeStringForLabelValue(host:port)
druidDiscoveryAnnouncement-cluster-identifier = <clusterIdentifier>
```
- Annotation:
```YAML
druidNodeInfo-<nodeRole.getJsonName()> = json_serialize(DiscoveryDruidNode)
```

For example:
- Labels -
```YAML
druidDiscoveryAnnouncement-broker = true
druidDiscoveryAnnouncement-id-hash = 14296512
druidDiscoveryAnnouncement-cluster-identifier = dev-druid-cluster
```
- Annotation -
```YAML
druidNodeInfo-broker = {
"druidNode": {
    "service": "druid/broker"
    "host": "test-host"
    "port" 80,
    ...
},
"nodeType": "broker",
...
```

- To watch all brokers, Watch All Pods with Following Labels:
```YAML
druidDiscoveryAnnouncement-broker = true
druidDiscoveryAnnouncement-cluster-identifier = dev-druid-cluster
```

Specifically, in the context of Kubernetes, when a Druid process starts up, it updates its Kubernetes pod definition with labels and annotations that help with node and service discovery. Here's how this works:
  - **Labels**: Labels in Kubernetes are key-value pairs associated with resources. The Druid process adds labels to its pod definition to indicate its role (e.g., "broker"), identity, and cluster identifier. For example, labels like "druidDiscoveryAnnouncement-broker" and "druidDiscoveryAnnouncement-cluster-identifier" are set to announce the role of the node and the cluster it belongs to.
  - **Annotations**: Annotations in Kubernetes are metadata associated with resources. Druid adds annotations to its pod definition to provide detailed information about its node or service. These annotations include information like the Druid node's service, host, port, and other relevant data.
  - **Watching Brokers**: To discover all brokers within the cluster, other components or processes (e.g., brokers, coordinators) use Kubernetes API calls to watch pods with specific labels, such as "druidDiscoveryAnnouncement-broker" and "druidDiscoveryAnnouncement-cluster-identifier." This allows them to identify and discover all Druid brokers running in the same cluster.
Overall, the combination of these pluggable discovery and leadership interfaces, along with Kubernetes labels and annotations, enables Druid to effectively manage node and service discovery and leadership coordination within a Kubernetes environment. This approach provides a flexible and extensible way to work with Kubernetes for these purposes.


## Leader Election:
- Leader Election Algorithm:
  - **Lease based Leader Election Algorithm**: In a lease-based leader election algorithm, leadership is granted to a candidate for a specific duration known as a lease. The candidate that successfully acquires a lease is designated as the leader.
  - Uses Atomic Test-and-Set/Compare-and-Swap provided by centralized Distributed Coordination System
  - All candidates try to test-and-set value, winner succeeds and becomes leader
  - **Atomic Test-and-Set/Compare-and-Swap**: The algorithm uses atomic test-and-set or compare-and-swap operations to establish leadership. This ensures that only one candidate succeeds in becoming the leader, as it can atomically update a value or resource that represents the leadership status.
  
- **Druid: Leader Election with K8S**
  - All k8s resources have a built-in field "resourceVersion"
  - UpdateRsource(<knownResourceVersion>, updates) is Atomic test-and-set operation
- We create a configMap resource, all candidates try to write following annotation using test-and-set, whoever succeeds, becomes the leader

```YAML
apiVersion: v1
kind: ConfigMap
metadata:
  annotations:
    control-plane.alpha.kubernetes.io/leader: '{"holderIdentity":"http://10.244.0.13:8088","leaseDurationSeconds":60,"acquireTime":"20231006T043506.012Z","renewTime":"20231006T093308.553Z","leaderTransitions":1}'
  name: druid-it-leaderelection-coordinator
  namespace: druid
```
- **Etcd vs K8S Api**:
  - Most users deploy druid on Cloud Vendor Managed K8S, and don't have access to Etcd

The leader election in the Druid-K8s extension works by utilizing Kubernetes API features and the "lease-based leader election" algorithm. Here's a brief explanation of how it functions:

- **Kubernetes ResourceVersion**: All Kubernetes resources (e.g., ConfigMaps, Pods, Services) have a built-in field called "resourceVersion." This field is used to track changes and updates to Kubernetes resources. It's a crucial component for maintaining consistency in a distributed system.

- **UpdateResource Operation**:
  - The leader election in Druid is implemented using Kubernetes resources and the "UpdateResource" operation. This operation is atomic and allows candidates to test and set a resource.
  - Candidates use "UpdateResource" with a specified "knownResourceVersion" to perform the test-and-set operation. This is similar to the compare-and-swap operation in distributed systems.

- **Atomic Test-and-Set**: In the context of Kubernetes, the extension uses an "Atomic Test-and-Set" operation, similar to the "Compare-and-Swap" (CAS) operation, provided by the centralized Distributed Coordination System.

- **Leader Election via ConfigMap**: To perform leader election, the extension creates a Kubernetes ConfigMap resource. This ConfigMap contains an annotation named "control-plane.alpha.kubernetes.io/leader," which contains details about the leader's identity, lease duration, and other relevant information.

- **Leadership Acquisition**: Candidates for leadership in the Druid cluster attempt to write the leader annotation in the ConfigMap. They do this using the Atomic Test-and-Set operation provided by Kubernetes. This operation is used to atomically update the annotation in the ConfigMap.

- **Successful Leader**: The candidate that successfully performs the Atomic Test-and-Set operation becomes the leader. The leader's information is recorded in the leader annotation, including details such as its identity, lease duration, acquisition time, renewal time, and leader transitions.

- **Lease-Based Algorithm**: The leader election in this extension follows a lease-based algorithm. The lease duration specified in the leader annotation determines how long a leader can hold the leadership position. The leader periodically renews its lease, and if it fails to do so, a new leader election is triggered.

- **Library for Leader Election**: The leader election functionality in the Druid-K8s extension may use a library like "k8s.io/client-go/tools/leaderelection" to help manage the leader election process.

The advantage of using Kubernetes for leader election in this extension is that it aligns with Kubernetes-native approaches and doesn't require direct access to an external component like etcd. Kubernetes is commonly used in cloud-managed Kubernetes environments, and this approach simplifies leader election in a Kubernetes deployment of Druid.

In summary, the leader election in the Druid-K8s extension leverages Kubernetes resources, annotations, and built-in features to implement leader election using a lease-based algorithm and the Atomic Test-and-Set operation. This allows for the seamless and Kubernetes-native management of leadership within the Druid cluster running on Kubernetes.

### Leader Election Mechanism:
The "UpdateResource" operation is used as part of the leader election mechanism. This mechanism typically involves the following steps:
- **Initialization**: When the Druid cluster starts up or when leader election is initiated, a specific Kubernetes resource, such as a ConfigMap, is created or identified for leader election. This resource contains the information that designates the leader.
- **ResourceVersion Check**: Candidates for leadership (representing different Druid components or nodes) concurrently attempt to perform an "UpdateResource" operation on this resource. As part of this operation, they specify the "knownResourceVersion" of the resource. The "knownResourceVersion" is typically set to the resource's current "resourceVersion."
- **Atomic Test-and-Set Operation**: The "UpdateResource" operation can be seen as an atomic test-and-set operation. It checks the current "resourceVersion" to ensure that the candidate knows the latest state of the resource. If the "knownResourceVersion" provided by the candidate matches the current "resourceVersion" of the resource, it implies that the candidate is aware of the latest state of the resource and can proceed with the update.
- **Leader Selection**: The candidate that successfully completes the "UpdateResource" operation (i.e., successfully updates the resource while specifying the correct "knownResourceVersion") becomes the leader. This leader is responsible for making critical decisions and coordinating activities within the Druid cluster.
- **ResourceVersion for Consistency**: The "resourceVersion" of the Kubernetnetes resource is crucial for ensuring consistency in the leader election process. It prevents race conditions by ensuring that only one candidate becomes the leader, as the others will fail to update the resource if their "knownResourceVersion" is outdated.

In summary, the "resourceVersion" and the "UpdateResource" operation are used to implement a form of leader election within the Kubernetes environment. They ensure that leadership is established and maintained in a consistent and coordinated manner, with only one candidate becoming the leader based on the outcome of the "UpdateResource" operation.

### etcd:
- the leader election mechanism in the Druid-K8s extension does not use etcd directly. Instead, it relies on Kubernetes-specific resources and features for leader election. In this approach, a ConfigMap with annotations is used to record the leader's information, and the leadership is established and managed within the Kubernetes environment.

### Configurations:
- `druid.discovery.type=k8s`: 
  - Setting druid.discovery.type to "k8s" (Kubernetes) indicates that Druid should use Kubernetes-native service discovery mechanisms to locate and interact with other services within your Kubernetes cluster. This is especially useful when you want to deploy Druid in a Kubernetes environment without relying on external service discovery systems like ZooKeeper.
  - When configured with druid.discovery.type=k8s, Druid components use Kubernetes service endpoints and DNS resolution to discover and communicate with other Druid services running in the same Kubernetes cluster. Kubernetes provides automatic service discovery and load balancing through its DNS service and service endpoints, which makes it a suitable choice for service discovery in a Kubernetes environment.
  - By using Kubernetes for service discovery, Druid can dynamically locate and connect to other services, which simplifies the deployment and scaling of Druid within Kubernetes. It eliminates the need for an external service discovery system like ZooKeeper or etcd, making Druid deployment more cloud-native and aligned with the Kubernetes ecosystem.
- `druid.discovery.k8s.clusterIdentifier=druid-it-1`:
  - The druid.discovery.k8s.clusterIdentifier configuration parameter in Druid is used to specify the Kubernetes cluster identifier. This identifier helps differentiate different clusters within a larger environment. When deploying multiple Druid clusters within a single Kubernetes environment, each cluster can have its own unique identifier, which can be set using this configuration parameter.
  - For example, if you are managing multiple Druid clusters (e.g., "dev-druid-cluster" and "prod-druid-cluster") within the same Kubernetes environment, you can set druid.discovery.k8s.clusterIdentifier to "druid-it-1" for one cluster and something different, such as "druid-prod-1," for the other. This ensures that Druid components within each cluster use a distinct cluster identifier for service discovery and communication, preventing any accidental interference between the clusters.
  - By providing a unique cluster identifier, you can isolate the service discovery namespace for each Druid cluster, even if they share the same Kubernetes environment. This configuration is particularly useful when you want to maintain separation and isolation between different environments or applications running within the same Kubernetes cluster.
- `druid.serverview.type=http`:
  - The druid.serverview.type configuration parameter in Druid specifies the type of server view to be used for communication between Druid nodes. When set to "http," it indicates that Druid nodes should communicate with each other and share server views using HTTP.
  - In a Druid cluster, the server view is responsible for sharing information about the available nodes and their status. Using "http" as the server view type means that HTTP endpoints are used for communication and coordination between the Druid nodes. This HTTP-based communication can be useful in various deployment scenarios, including Druid deployments on Kubernetes.
  - With the "http" server view type, Druid nodes exchange information about the available segments, historical nodes, and other cluster-related details via HTTP requests and responses. This configuration is particularly relevant when deploying Druid in environments where HTTP communication is the preferred or most practical method for coordinating node interactions.
- `druid.coordinator.loadqueuepeon.type=http`:
  - The druid.coordinator.loadqueuepeon.type configuration parameter in Druid specifies the type of Load Queue Peon to be used by the Druid Coordinator. A Load Queue Peon is responsible for handling the assignment of segments to historical nodes and managing the load queue in a Druid cluster.
  - When set to "http," it indicates that the Load Queue Peon uses HTTP for communication and coordination. This means that the Druid Coordinator, responsible for managing the assignment of segments to historical nodes, communicates with the Load Queue Peon using HTTP requests and responses.
  - In a Druid cluster, the Load Queue Peon helps in distributing segments efficiently across historical nodes, balancing the load, and ensuring that the historical nodes receive the appropriate segments to process. Using HTTP for communication can be advantageous in Kubernetes or other environments where HTTP-based communication is more suitable for coordinating these tasks.
  - So, when druid.coordinator.loadqueuepeon.type is set to "http," it means that the Druid Coordinator will use HTTP to communicate with the Load Queue Peon for segment assignment and management in the cluster. This configuration is relevant when deploying Druid on Kubernetes without relying on ZooKeeper for coordination.
- `druid.indexer.runner.type=httpRemote`
  - The druid.indexer.runner.type configuration parameter in Druid specifies the type of Indexer Runner that Druid will use to manage tasks related to data indexing. An Indexer Runner is responsible for running indexing tasks, which are used to ingest and index data into Druid's storage.
  - 
## Resources:
- https://www.youtube.com/watch?v=TRYOvkz5Wuw
- https://github.com/apache/druid/issues/9053
- https://github.com/apache/druid/pull/10544
- https://druid.apache.org/docs/latest/configuration/#segment-management
￼
￼
￼
