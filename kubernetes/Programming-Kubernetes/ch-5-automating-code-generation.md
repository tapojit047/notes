## Boilerplate Code:
- Boilerplate code refers to a block of code that is used as a starting point for new projects or features. This code is typically generic and can be reused across multiple projects or features. Examples of boilerplate code include code for connecting to a database, code for handling user authentication, or code for setting up a web server.
- Boilerplate code is usually simple, well-tested, and easy to understand, making it a useful starting point for developers. It can save time and effort when starting new projects, as developers do not have to write the same basic functionality from scratch every time. It also promotes consistency and can help to ensure that best practices and standards are followed across different projects.
- Boilerplate code can be generated manually or with the help of code generation tools, templates, or frameworks. It can be also used as a library, package or a module which can be reused.

## runtime.Object:
- ``runtime.Object`` is an interface defined in the Go programming language in the Kubernetes project. It defines a set of methods that an object must implement in order to be considered a "runtime object."
- The ``runtime.Object`` interface is a key building block in the Kubernetes API and is used to define the structure of the resources that can be manipulated by the API. It is also used to define the structure of the objects that are passed between components of the Kubernetes system.

## Four standard code generators for CRs:
### deepcopy-gen:
- deepcopy-gen is a code generator for the Go programming language that creates a DeepCopy method for types that implement the runtime.Object interface from the Kubernetes project. This method creates a deep copy of the object, meaning that all of its fields are also copied recursively.

### client-gen:
- client-gen is a tool that is used to generate client code for the custom resource in Go language.
- Creates typed client sets.

### informer-gen:
- an informer is a component that watches the Kubernetes API server for changes to a specific resource type, and then caches and exposes those changes to other parts of the system.
- ``informer-gen`` Creates informers for CRs that offer an event-based interface to react to changes of CRs on the server.
- ``informer-gen`` is a tool that can be used to generate the code for an informer for a custom resource. It takes as input the definition of the custom resource in the form of a Kubernetes Custom Resource Definition (CRD) and generates Go code for an informer that can be used to watch and receive updates for instances of that custom resource.
- This tool is useful when you have a custom resource that you want to monitor and respond to changes in the same way as built-in Kubernetes resources. By using an informer, you can avoid the need to constantly poll the API server for changes, and instead receive updates in a more efficient and scalable manner.

### lister-gen:
- lister-gen is a tool that can be used to generate the code for a lister for a custom resource. It takes as input the definition of the custom resource in the form of a Kubernetes Custom Resource Definition (CRD) and generates Go code for a lister that can be used to list instances of that custom resource. This lister can be used to filter, sort, and paginate the instances of the custom resource.

