# Druid-K8S-extension:

## How Leader Selection works:
- Leader Election:
- Leader Election Algorithm:
  - Lease based Leader Election Algorithm
  - Uses Atomic Test-and-Set/Compare-and-Swap provided by centralized Distributed Coordination System
  - All candidates try to test-and-set value, winner succeeds and becomes leader
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

- **Kubernetes ResourceVersion**: All Kubernetes resources have a built-in field called "resourceVersion." This field is used to track changes and updates to Kubernetes resources. It's a crucial component for maintaining consistency in a distributed system.

- **Atomic Test-and-Set**: In the context of Kubernetes, the extension uses an "Atomic Test-and-Set" operation, similar to the "Compare-and-Swap" (CAS) operation, provided by the centralized Distributed Coordination System.

- **Leader Election via ConfigMap**: To perform leader election, the extension creates a Kubernetes ConfigMap resource. This ConfigMap contains an annotation named "control-plane.alpha.kubernetes.io/leader," which serves as a record of the leader election state.

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


### ZooKeeper Use Case:
- **State Synchronization**:
  - Segment Assignment (Load/Dop) to Historical Nodes
  - Segment Announcements by DataNodes
  - Task Assignment
  - Task Runtime State and Status
- **Other**:
  - Node/Service Discovery
  - Leader Election

###  Druid: State Synchronization with ZooKeeper:
![Screenshot from 2023-10-12 17-44-19.png](..%2F..%2F..%2FPictures%2FScreenshots%2FScreenshot%20from%202023-10-12%2017-44-19.png)

