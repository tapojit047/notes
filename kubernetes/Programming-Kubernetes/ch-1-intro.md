## Kubernetes-native app: 
- A Kubernetes-native application is a software application that is designed to run on and take full advantage of the features provided by the Kubernetes container orchestration system. This typically means that the application is broken down into a set of smaller, modular components, known as "pods," which can be easily deployed, scaled, and managed using Kubernetes.
- Kubernetes-native applications are typically developed using a microservices architecture, where each component or "service" runs in its own container, and communicates with other services via a well-defined API. This allows for greater flexibility and scalability, as individual components can be updated or replaced without affecting the entire application. 

## Controller:
- A controller implements a control loop,
watching the shared state of the cluster through the API server and making
changes in an attempt to move the current state toward the desired state.
- In Kubernetes, a controller is a control loop that continuously monitors the desired state of the system and makes changes to the actual state to bring it in line with the desired state. Controllers are responsible for ensuring that the resources in a Kubernetes cluster are in the desired state. Controllers are implemented as control loops that watch the state of the cluster, and make changes to bring the actual state in line with the desired state.
- Kubernetes has several built-in controllers, such as: ReplicationController, Deployment, StatefulSet, DaemonSet
- Data structures used by Controller:
  - Informers
  - Work queues

## Custom  resource:
- In Kubernetes, a custom resource is an extension of the Kubernetes API that allows users to define their own resource types, along with their own fields and validation rules. Custom resources are used to store and manage the desired state of application-specific or infrastructure-specific objects that are not natively supported by Kubernetes.
- Custom resources are defined using the Kubernetes API conventions and are stored in the Kubernetes cluster just like built-in resources (such as Pods, Services, and ReplicationControllers).
- Custom resources are typically used in conjunction with Kubernetes controllers, which are responsible for ensuring that the actual state of the custom resources in the cluster matches their desired state. 
- An example of a custom resource is a custom resource definition (CRD) for a database service, where the CRD defines the fields for the database service such as name, number of replicas and storage size.

## Operator:
- In Kubernetes, an operator is a software extension that uses Kubernetes' custom resource and controller features to manage specific, complex application or infrastructure. 
- An operator is essentially a piece of software that automates the management of a specific type of application or service. It does this by translating the desired state of the application as specified in Kubernetes manifests into the necessary actions on the underlying infrastructure.
- We call this new class of software Operators. An Operator is an
application-specific controller that extends the Kubernetes API to
create, configure, and manage instances of complex stateful
applications on behalf of a Kubernetes user. It builds upon the basic
Kubernetes resource and controller concepts but includes domain or
application-specific knowledge to automate common tasks.
- [Video Nana](https://www.youtube.com/watch?v=ha3LjlD6g7g)
- [Video IBM](https://www.youtube.com/watch?v=i9V4oCa5f9I)

## Control loop:
- No matter how complex or simple your controller is, these three steps—read
resource state ˃ change the world ˃ update resource status—remain the
same.

## Watch Event:
- In Kubernetes, a watch event is a notification that is generated when a specific resource in the cluster changes. Watch events are used by controllers and operators to monitor the state of the cluster and take appropriate action.

## Event Object:
- In Kubernetes, an event object is a record of an occurrence in the cluster that is of interest to the system administrator or operators.
- Event objects contain information about the resource that caused the event, the type of event that occurred, and the reason for the event. The event object also includes a timestamp and an optional message that provides additional details about the event.
- The top-level Event object is a resource like pods,
deployments, or services, with the special property that it has a
time-to-live of an hour and then is purged automatically from
etcd.

## Optimistic Concurrency:
- Optimistic concurrency is a technique used to manage conflicts that can arise when multiple users or processes attempt to update the same piece of data simultaneously. The basic idea behind optimistic concurrency is to allow each user or process to make changes to the data without first checking if other users or processes are also making changes. Conflicts are then detected and resolved when the changes are committed.
- Kubernetes API server uses optimistic concurrency.