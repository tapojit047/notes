## API-Group:
- In the context of Kubernetes, an API group is a collection of related resources that are accessed through the Kubernetes API. Each resource is identified by a unique URL path and can be manipulated using the standard HTTP methods (GET, POST, PUT, DELETE, etc.).
- The Kubernetes API is organized into several groups, each of which contains a set of related resources. For example, the "core" group contains resources such as pods and services, while the "apps" group contains resources such as Deployments and StatefulSets.
- Each group also has a version, so for example the versioned group would be ``core/v1`` and ``apps/v1``.

## How the API Server Processes Requests:
The Kubernetes API Server is the component responsible for handling incoming requests and interacting with the Kubernetes cluster. When a request is made to the API Server, it goes through several stages of processing:
- Authentication: The API Server checks the credentials of the user making the request, and verifies that they have the appropriate permissions to perform the action they are requesting.
- Authorization: The API Server checks the user's permissions to ensure they are authorized to perform the action they are requesting.
- Validation: The API Server validates the request to ensure that it is well-formed and contains all the necessary information.

- Admission Control: The API Server runs a set of validators and mutators that can modify or reject the request.

- Execution: The API Server performs the requested action, such as creating, updating, or deleting a resource.

- Response: The API Server returns a response to the user, indicating whether the request was successful or not, and providing any additional information.

The API Server uses etcd as the storage backend which stores all the objects in the cluster, and it uses the Kubernetes API objects to interact with the cluster. The API Server also implements the Kubernetes API and serves as a bridge between the user and the cluster.