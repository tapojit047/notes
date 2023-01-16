## API:
- The REST API is the fundamental fabric of Kubernetes. All operations and communications between components, and external user commands are REST API calls that the API Server handles. Consequently, everything in the Kubernetes platform is treated as an API object and has a corresponding entry in the API.
- The Kubernetes API is a resource-based (RESTful) programmatic interface provided via HTTP. It supports retrieving, creating, updating, and deleting primary resources via the standard HTTP verbs (POST, PUT, PATCH, DELETE, GET).

## K8s API terminology:
- A resource type is the name used in the URL (``pods``, ``namespaces``, ``services``)
- All resource types have a concrete representation (their object schema) which is called a kind
- A list of instances of a resource is known as a collection
- A single instance of a resource type is called a resource, and also usually represents an object
- For some resource types, the API includes one or more sub-resources, which are represented as URI paths below the resource

**Note (i):** Some objects are not namespaced (for example: Nodes), and so their names must be unique across the whole cluster.

**Note (ii):** The Kubernetes API allows clients to make an initial request for an object or a collection, and then to track changes since that initial request: a watch. Clients can send a list or a get and then make a follow-up watch request.

## Resource deletion:
When you delete a resource this takes place in two phases.
    
    1. finalization

    2. removal

- When a client first sends a delete to request removal of a resource, the .metadata.deletionTimestamp is set to the current time. Once the .metadata.deletionTimestamp is set, external controllers that act on finalizers may start performing their cleanup work at any time, in any order.
- Once the last finalizer is removed, the resource is actually removed from etcd.

