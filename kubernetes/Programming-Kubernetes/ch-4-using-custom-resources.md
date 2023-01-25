## Custom Resources:
- A resource is an endpoint in the Kubernetes API that stores a collection of API objects of a certain kind; for example, the built-in pods resource contains a collection of Pod objects.
- In Kubernetes, a custom resource is a user-defined resource that extends the Kubernetes API. Custom resources allow you to define your own resource types, beyond the built-in Kubernetes resource types such as pods, services, and deployments. These custom resources are managed by custom controllers, which are responsible for performing actions on the custom resources, such as creating, updating, or deleting them.
- Custom resources can be defined by creating a custom resource definition (CRD) that specifies the properties and validation rules for the custom resource. Once a CRD is created, you can use kubectl to create, update, and delete instances of the custom resource, just like you would with built-in resources.
- Custom resources are useful for extending Kubernetes to support specific use cases, such as managing custom application configuration or adding additional functionality to Kubernetes.
- A CustomResourceDefinition (CRD) is a Kubernetes resource itself. It
describes the available CRs in the cluster.

## Custom Controller:
- In Kubernetes, a custom controller is a piece of software that watches for changes to a custom resource and performs actions based on those changes. Custom controllers are used in conjunction with custom resources, which are user-defined resources that extend the Kubernetes API.
- Custom controllers can be written in any programming language, and they are typically implemented as a loop that continuously watches the Kubernetes API for changes to the custom resource. Custom controllers can also be built using Kubernetes operator framework, which provides a way to build controllers that are more robust and easier to maintain.
- On their own, custom resources let you store and retrieve structured data. When you combine a custom resource with a custom controller, custom resources provide a true declarative API.

## API Aggregation:
- API aggregation refers to the process of combining multiple APIs into a single, unified API. This can be done for a variety of reasons, such as to simplify the developer experience, to increase security, or to improve performance.]
- In Kubernetes, API aggregation refers to the process of exposing multiple custom resources as a single, unified API. This can be done by creating a Custom Resource Definition (CRD) for each custom resource, and then using an API aggregation controller to expose them as a single API.
- API aggregation in Kubernetes enables users to interact with multiple custom resources using the same command-line interface, programming libraries, and other tools they use to work with built-in Kubernetes resources. This can simplify the developer experience by reducing the number of different APIs that need to be understood and used.
- API aggregation in Kubernetes is typically done by creating a custom controller that watches for changes to the custom resources, performs actions based on those changes, and reflects the changes in the Kubernetes API. This controller can be built using Kubernetes operator framework, which provides a way to build controllers that are more robust and easier to maintain.

## Finalizer:
- In Kubernetes, a finalizer is a special type of annotation that can be added to a custom resource to allow for additional cleanup actions to be performed before the resource is deleted.
- When a resource is deleted, the Kubernetes API server first checks if the resource has any finalizers. If it does, it will perform the cleanup actions specified by the finalizer before actually deleting the resource. This allows for additional steps to be taken to ensure that the resource's deletion does not leave any resources in an inconsistent state.

## Validation:
- In Kubernetes, validation is the process of ensuring that a custom resource conforms to the specification defined in its CustomResourceDefinition (CRD). When a custom resource is created, updated, or deleted, the Kubernetes API server validates the resource against the CRD's schema to ensure that it is well-formed and conforms to the expected structure and format.


## Dynamic Client:
- ``Client-go`` includes a dynamic client package, which allows developers to interact with the Kubernetes API using the ``unstructured.Unstructured type``, which is a generic representation of a Kubernetes resource. This allows developers to work with Kubernetes resources in a more flexible and dynamic way, as they can manipulate and interact with resources without needing to know their specific schema or structure. The dynamic client also allows developers to create, update, and delete resources without having to manually construct the JSON or YAML for the resource.

## Typed Client:
- Typed clients do not use ``map[string]interface{}``-like generic data structures but instead use real Golang types, which are different and specific for each GVK.
- They are much easier to use, have considerably increased type safety, and make code much more concise and readable.