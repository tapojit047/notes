## API Machinery:
- k8s.io/apimachinery/pkg/apis/meta/v1
- It includes all the generic building blocks to implement
a Kubernetes-like API

## kubeconfig file:
- A kubeconfig file is a configuration file used to connect to a Kubernetes cluster. It is typically used by command-line tools such as kubectl, the Kubernetes command-line client, and other Kubernetes-related tools. The file contains information such as the server URL, certificate authority data, and authentication credentials for the cluster.
- The kubeconfig file is typically stored in the user's home directory, in a subdirectory called ".kube". It can contain information for multiple clusters, and multiple users, so that the user can switch between clusters and users easily. The file is in the YAML format. Each entry in the file is called a context. A context is a combination of a cluster, a user, and a namespace.
- It's used to configure access to a Kubernetes cluster, it stores information such as the server URL, certificate authority data, and authentication credentials. The kubeconfig file is used by the kubectl command-line tool to connect to the cluster and by other Kubernetes-related tools, it is also used for authentication when using Kubernetes API.

## Config Object: (BuildConfigFromFlags)
- This config object can be used to create a Kubernetes client, which can be used to perform various operations on the cluster such as creating, updating, and deleting resources.

## Clientset object:
- The Clientset object is used to perform various operations on the cluster such as creating, updating, and deleting resources. It also allows to access different APIs in Kubernetes such as pods, services, deployments, and more.

## API group:
- In Kubernetes, an API group is a set of resources that are grouped together based on their functionality. Each resource within an API group has a unique URL endpoint, and the API group name is included in the URL. For example, the URL endpoint for a Deployment resource in the "apps" API group would be "https://kubernetes.default.svc/apis/apps/v1/deployments". Kubernetes includes several built-in API groups, such as "apps", "batch", and "extensions", and you can also create custom API groups for your own resources.

## API group version:
- An API group version in Kubernetes refers to a specific version of an API group. Each API group version defines a set of resources and their associated properties, and the API group version is included in the URL endpoint for each resource. For example, the URL endpoint for a Deployment resource in the "apps" API group version "v1" would be "https://kubernetes.default.svc/apis/apps/v1/deployments".
- Api group version is used for backward compatibility. When a new version of the API is released, it is added as a new API group version, so that the previous version can still be used by clients that are not yet compatible with the new version. As time goes on, the old API group versions may be deprecated and eventually removed.
- In summary API Group Version is a combination of API Group name and the version of API, it's used to identify the specific version of API group and resources within that API group.

## Kubernetes objects in GO:
- In Go, Kubernetes objects are typically represented as structs that define the fields and properties of the object. The Kubernetes API is accessed through the Go client library, which provides a set of functions for creating, updating, and deleting Kubernetes objects, as well as for retrieving information about them.
- The Go client library also includes structs for Kubernetes API resources such as pods, services, and deployments. These structs can be used to define the desired state of a Kubernetes object, and then passed to the client library's functions for creating, updating, or deleting the object.
- Additionally, there are many open-source libraries built on top of the Kubernetes Go client library, which provide additional functionality and abstractions for working with Kubernetes objects in Go. These libraries include libraries like kubebuilder, operator-sdk, client-go, and many more.

## Metadata:
- In Kubernetes, metadata is a set of data that describes an object and its properties. The metadata of a Kubernetes object includes information such as its name, labels, and annotations.
- The metadata of a Kubernetes object can be divided into two main parts:
    - **Object metadata**: This includes information about the object itself, such as its name, namespace, and UID.
    - **Object specification metadata**: This includes information about the desired state of the object, such as its labels and annotations, and the specification of the container or pod.
- Object metadata is used to uniquely identify and locate an object, while object specification metadata is used to define the desired state of the object and its properties.
- Labels and annotations are two types of metadata that are commonly used in Kubernetes to add additional information to objects. Labels are key-value pairs that can be used to organize and group objects, while annotations are arbitrary key-value pairs that can be used to add additional information to an object.
- In summary, metadata in Kubernetes is a set of data that describes an object and its properties, including information such as its name, labels, and annotations. This metadata is used to uniquely identify and locate objects, as well as to define the desired state of the objects and their properties.

## TypeMeta:
- TypeMeta is a struct that is included in many Kubernetes objects in the Go client library. It defines metadata about the object's type, such as its API version and kind.
- The TypeMeta struct includes two fields:
     - **APIVersion**: This field specifies the version of the API group that the object belongs to.
     - **Kind**: This field specifies the kind of the object, such as "Pod" or "Service".
- The TypeMeta struct is used to ensure that the correct version of an API group is used when creating or updating an object, and to identify the type of an object when it is retrieved from the Kubernetes API.
- It is used as a common struct for many kubernetes objects, and it helps in identifying the object, its API version and Kind. It is used to identify the specific version of the API group that the object belongs to, and to ensure that the correct version of the API group is used when creating or updating the object.
- In summary, TypeMeta is a struct that provides metadata about the type of a Kubernetes object, including its API version and kind, and is commonly used across many Kubernetes objects in the Go client library.

## ObjectMeta:
- ``ObjectMeta == metadada in YAML``
- In Kubernetes, ObjectMeta is a field in the API objects that are used to represent resources in the cluster. It contains metadata about the resource, such as its name, namespace, labels, and annotations. The ObjectMeta field is a common field across all Kubernetes objects, and is used to provide information about the object's state and configuration.

## ClientSet:
- In Kubernetes, a client set (often referred to as "clientset") is a Go package that provides a programmatic interface to the Kubernetes API. It allows developers to interact with the Kubernetes cluster and perform operations on resources such as pods, services, and deployments.
- Using a clientset, developers can perform operations such as creating, reading, updating, and deleting resources in the Kubernetes cluster. The clientset also includes helper functions for common tasks such as listing resources, watching for changes, and handling errors.
- It is a common practice to create a single instance of clientset and reuse it throughout the application to interact with the Kubernetes cluster, this way it eliminates the overhead of creating multiple clientsets.
- To create a clientset from a config file ``clientset, err := kubernetes.NewForConfig(config)``

## Informers:
- In Kubernetes, an informer is a mechanism for caching and synchronizing resources from the Kubernetes API. An informer periodically polls the API server for updates to a particular resource type, and then updates its local cache with the latest information. This allows clients to consume the data from the cache instead of querying the API server directly, which can be more efficient and reduce the load on the API server.
- Informers are implemented as Go objects and are typically created by the client-go library. The library provides a set of informer factories for different resource types, such as pods, services, and deployments. The informer factory can be used to create an instance of an informer for a specific resource type, namespace, and set of options.
- Informers are designed to work with Kubernetes controllers, which are responsible for managing the state of resources in the cluster. A controller can use an informer to watch for changes to a particular resource type and take actions based on those changes. For example, a deployment controller might use an informer to watch for updates to deployments and then scale up or down the number of replicas based on the current state.
- Informers are also a powerful feature of Kubernetes, they can be used to watch for changes to multiple resources, and it is possible to create multiple informers for the same resource type but with different filters.
- In summary, informers and caching in Kubernetes provide an efficient way to synchronize resources from the Kubernetes API and reduce the load on the API server. They are used in conjunction with controllers to manage the state of resources in the cluster and watch for changes to those resources.
- A controller that accesses the API server every time it needs an object creates a high
load on the system. In-memory caching using informers is the solution to this problem.
Moreover, informers can react to changes of objects nearly in real-time instead of
requiring polling requests.

## Work Queue:
- A work queue in Kubernetes is a data structure that stores a list of tasks to be executed. It is used to manage and distribute workloads among different nodes in a cluster. In Kubernetes, work queues are used to manage the scheduling and execution of pods, which are the basic units of work in the system. The Kubernetes scheduler uses the work queue to determine where to place pods, and to ensure that they are running on the appropriate nodes. This helps to ensure that the cluster is used efficiently and that workloads are distributed in a balanced way.
- The following queue types are derived from this generic interface:
    - **DelayingInterface** can add an item at a later time.
    - **RateLimitingInterface**:
      - It rate-limits items being added to the queue. It extends the ``DelayingInterface``. 
      - **Rate Limiter**: 
        - A rate limiter is a tool that is used to control the rate at which items are added to a work queue. It is used to prevent a work queue from becoming overloaded and to ensure that the system remains stable and responsive.
        - A rate limiter works by controlling the rate at which items are added to the work queue by monitoring the number of items added per unit of time. If the rate exceeds a certain threshold, the rate limiter will block or delay the addition of new items until the rate drops below the threshold again. This helps to prevent the work queue from becoming overwhelmed, and ensures that the system can continue to process items at a steady pace.
        - In the context of the RateLimitingInterface interface, rate limiter is used to limit the number of items added to the work queue per unit of time. The AddRateLimited(item interface{}) method is used to add an item to the work queue after checking with the rate limiter that it's okay to do so. The rate limiter can be implemented in different ways, for example using a token bucket algorithm, leaky bucket algorithm or fixed window algorithm.

## API Machinery:
### GroupVersionKind(GVK):
- Together, the group, version and kind fields form a unique identifier for a resource that can be used to distinguish it from other resources in the Kubernetes API. GVK is used to determine which resources are available in an API and how to interact with them. It is used by the Kubernetes client-go library and the kubectl command-line tool to determine the type of a resource, and it is also used by the Kubernetes API server to route requests to the appropriate controller.
- Also, the Kubernetes API server uses the GVK to determine which controller should handle the request. The controller is responsible for handling the requests and updating the state of the resources, rather than the API server itself.
- While the Kind field of a GVK is an important aspect of identifying a resource in the Kubernetes API, it does not map one-to-one to specific HTTP paths.

### GroupVersionResource(GVR):
- GroupVersionResource (GVR) is a combination of a resource's group, version, and resource name, it's used to uniquely identify a resource within the Kubernetes API and it's used in many parts of the Kubernetes API and client libraries.
- A resource's group is a logical grouping of resources, such as "apps" or "batch". A resource's version is the version of the API that the resource belongs to, such as "v1" or "v1beta1". The resource name is the actual name of the resource, such as "pods" or "services".

### REST Mapping:
- The mapping of a GVK to a GVR is called REST mapping.

### Scheme:
- A scheme in kubernetes is a set of types, functions and methods that are used to convert between the internal representation of resources and the external representation of resources in the API. It provides the mechanism to encode and decode the resources in a way that can be understood by the cluster and the client.
- The internal representation is the struct type that is used by the k8s client-go library to represent the resource in the Go code and the external representation is the JSON or YAML representation of the resource that is sent and received over the API.

![alt text](https://github.com/tapojit047/notes/blob/master/kubernetes/images/chap3.png)

## Vendoring:
- Vendoring is the process of including third-party dependencies (also called "vendors") directly in a project's source code repository, rather than relying on them to be installed separately on the system where the project will be built or run.
- In Go, vendoring is typically done by creating a "vendor" directory within the project's source code repository, and then copying the dependencies' source code into that directory. This allows the project to include the dependencies as part of its source code, and it ensures that the same versions of the dependencies are used regardless of the environment where the project is built or run.
- Vendoring is useful in situations where the dependencies are not available through a package manager, or when you want to ensure that a specific version of a dependency is used, even if a newer version is available. It also helps in situations where the project needs to be built or run on an environment that is not connected to the internet.
- There are different tools and libraries that can be used to handle vendoring in Go, such as ``govendor``, ``dep``, and ``modules``. These tools automate the process of copying the dependencies' source code into the project's repository and managing the dependencies' versions.
- In summary, vendoring is the process of including third-party dependencies directly in a project's source code repository. It is done to ensure that the same versions of the dependencies are used, regardless of the environment where the project is built or run. Vendoring is commonly used in Go projects, and there are different tools and libraries that can be used to handle it.

### Glide: 
- Glide is a package manager for Go that helps to manage dependencies. It uses a "glide.yaml" file
- One of the main features of Glide is its "glide.yaml" file, which is used to specify the dependencies of a project. This file lists all of the dependencies, along with their version numbers, and Glide uses this information to ensure that the correct versions of the dependencies are installed and used.
- ``glide install -v`` 
- this command is used to install the dependencies of a Go project as specified in the project's "glide.yaml" file. The -v flag causes Glide to output detailed information about the installation process, and it creates a "glide.lock" file that locks the versions of the dependencies to the versions specified in the glide.yaml file.

### dep:
- dep is a dependency management tool for Go programming language, it allows developers to easily manage the dependencies of a project, including the ability to easily add, update, and remove dependencies, as well as to ensure that the correct versions of dependencies are used at all times. It also allows for reproducible builds by ensuring that everyone is using the same versions of dependencies. It uses Gopkg.toml and Gopkg.lock files to manage dependencies.

### GO modules:
- Go modules is a built-in dependency management system for the Go programming language that was introduced in Go 1.11. It is designed to make it easier to manage dependencies for Go projects. Go modules provide a way to manage dependencies by specifying the version of a package in the import statement of the code and it uses a go.mod file to list the dependencies and their versions. Go modules provide a number of benefits over traditional Go dependency management tools and it is built into the Go toolchain.
- With client-go v12.0.0—matching Kubernetes 1.15—we ship a go.mod file. The shipped go.mod file includes all dependencies, and your project
go.mod file no longer has to list all transitive dependencies manually.
