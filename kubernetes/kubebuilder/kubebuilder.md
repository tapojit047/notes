# kubebuilder
Kubebuilder is an open-source framework and set of tools designed to simplify and accelerate the development of Kubernetes-native applications. It is a project that aims to make it easier for developers to build and maintain Kubernetes custom resources, controllers, and operators. Custom resources and controllers are fundamental building blocks for creating custom functionality in Kubernetes.

Here are some key features and components of Kubebuilder::
- **Custom Resources (CRs)**: Kubebuilder helps you define custom resources, which are extensions of the Kubernetes API. These custom resources allow you to define and manage application-specific configurations and objects.
- **Controller Development**: Kubebuilder provides tools for developing custom controllers that watch and manage custom resources. Controllers are used to reconcile the desired state of custom resources with their actual state, ensuring that applications are deployed and maintained correctly.
- **Code Generation**: It offers code generation capabilities to automatically create boilerplate code for custom resources and controllers, saving developers time and reducing the potential for errors.
- **API Schemas**: Kubebuilder provides tools for defining the schema of custom resources, making it easier to validate and work with these resources.
- **Testing Framework**: It includes a testing framework that allows you to write unit tests for your custom controllers and resources.
- **Dependency Management**: Kubebuilder can help manage dependencies for your project, including those related to the Kubernetes libraries and client code.
- **Operator SDK Integration**: It can be used in conjunction with the Operator SDK, which is a set of tools for building Kubernetes operators. Operators are a pattern for deploying and managing complex, stateful applications on Kubernetes.

Kubebuilder simplifies the process of building operators and applications that leverage Kubernetes' declarative model. It encourages best practices, code reusability, and consistency in Kubernetes application development. This makes it a popular choice for building custom controllers and operators for managing applications and services on Kubernetes.

### Initializing a repo using kubebuilder:
- `go mod init`
- `go mod tidy && go mod vendor`
- **Command**: `kubebuilder init --domain my.domain --repo my.domain/guestbook`
The kubebuilder init command is used to initialize a new Kubebuilder project with the specified project settings. In the command above:
- `--domain my.domain`:  The --domain flag specifies the domain name for the project. This is typically the domain associated with your organization or project. For example, if your organization's domain is "example.com," you would replace "my.domain" with "example.com."
- `--repo my.domain/guestbook`: The --repo flag specifies the repository path for your project. This is typically in the format my.domain/project-name. Here, "my.domain" is a placeholder, and "guestbook" should be replaced with the actual name of your project.
- When you run this command, Kubebuilder initializes a new project with the specified domain and repository settings. This involves setting up the project directory structure, initializing version control (Git), and generating the initial project files.
- Here's a step-by-step breakdown of what this command does:
1. Project Directory Structure: Kubebuilder creates a project directory structure, including directories for code, configuration, and manifests.
2. Git Initialization: If not already initialized, Kubebuilder initializes a Git repository in the project directory.
3. Project Configuration: Kubebuilder generates a configuration file (usually PROJECT) that contains information about your project, including the domain name and repository path.
4. Generating Initial Files: Kubebuilder generates boilerplate code and configuration files for your project, including a main Go file, Dockerfile, Makefile, and other necessary files.
5. Git Commit: The command automatically commits the initial project files to your Git repository.

After running this command, you will have the foundation of a Kubebuilder project with the specified domain and repository settings. You can then proceed to add custom resources, controllers, and additional logic to build your Kubernetes operator or application as needed.

### Kustomize:
- Kustomize is a command-line configuration management tool for Kubernetes. It is used to customize, configure, and manage Kubernetes resources without directly modifying the original resource files. 
- In simple words, a "Kustomization" in the context of Kubernetes is like a recipe or a set of instructions for customizing your Kubernetes configuration. It tells Kubernetes how to take your basic configuration (the default settings) and make specific changes to it without actually altering the original files. These changes can be things like adding labels, modifying values, or including additional resources.
- Think of it as a way to easily tweak your Kubernetes setup for different purposes or environments, without having to manually edit all your configuration files every time you need a slight variation. It's a way to keep your configuration organized and adaptable.

### Scheme:
In the context of Kubernetes and the Kubernetes Go client libraries, a "scheme" is a core component used to define how Kubernetes API objects are serialized and deserialized (marshaled and unmarshaled) between their Go representations and their JSON or YAML representations. It is essentially a mapping between Go types and the Group-Version-Kind (GVK) identifiers used in Kubernetes. Here's what a scheme does and why it's important:

- GVK Mapping: A scheme maintains a registry of GVKs and their corresponding Go types. This mapping is crucial for the Kubernetes API server and client libraries to know how to handle specific resource types.
- Marshaling and Unmarshaling: When you interact with the Kubernetes API server or Kubernetes resources in your Go code, the scheme is responsible for converting Go objects into JSON or YAML representations for transmission (marshaling) and vice versa (unmarshaling). It ensures that the data is correctly converted back and forth.
- Custom Resources: Schemes are used extensively when working with custom resources created by operators or custom controllers. They help the client libraries understand how to work with these custom resource types.
- Versioning: Schemes allow for dealing with different API versions and groups. This is important because Kubernetes APIs may have multiple versions, and the scheme helps manage those differences.

Schemes are typically used in Kubernetes controller code, where the controller needs to work with different resource types and versions. Schemes abstract away the complexities of working with the Kubernetes API, making it easier for developers to build controllers and operators that interact with Kubernetes resources.

When you see code like Scheme: mgr.GetScheme() in a controller setup, it means that the controller is being configured with a scheme that defines how Kubernetes resources are represented in Go and how they should be processed. This scheme is critical for ensuring proper interaction with the Kubernetes API server and for maintaining the desired state of resources in a Kubernetes cluster.

### controller-runtime:
`controller-runtime` is a Go library provided by the Kubernetes community for building Kubernetes controllers. Kubernetes controllers are custom controllers that automate tasks and manage the state of resources within a Kubernetes cluster. The `controller-runtime` library simplifies the process of developing, testing, and running Kubernetes controllers by providing a framework with common functionalities. Here are some key features and components of the "controller-runtime" library:
- Reconciliation Loop: The library provides a framework for implementing the reconciliation loop, which is a key part of how controllers work. Controllers use this loop to ensure that the actual state of resources in the cluster matches their desired state.
- Event Handling: "controller-runtime" includes tools for efficiently watching and handling Kubernetes events (e.g., resource creation, updates, deletions). It uses informers to keep track of changes in resources and dispatch events to controllers.
- Leader Election: The library supports leader election mechanisms, ensuring that only one instance of a controller is active at a time. Leader election is important for achieving high availability and avoiding conflicts.
- Custom Resource Definitions (CRDs): The library helps manage Custom Resource Definitions, allowing you to define and operate on custom resources that extend the capabilities of Kubernetes.
By using `controller-runtime`, developers can build controllers in a more structured and consistent way, which simplifies the development and maintenance of controllers. The library abstracts many of the low-level details of interacting with the Kubernetes API server and allows developers to focus on the specific logic related to resource reconciliation. This can lead to more reliable and maintainable controllers in a Kubernetes environment.

### controller-runtime manager:
The `controller-runtime` manager is a core component of the controller-runtime library, which is a framework for building Kubernetes controllers in Go. The manager is responsible for coordinating the operation of controllers, ensuring that they are properly initialized, and handling various aspects of controller execution, including resource synchronization, event processing, and reconciliation. Here are some key responsibilities and functions of the `controller-runtime` manager:
- Controller Lifecycle Management: The manager manages the lifecycle of controllers. It initializes them, starts them, and handles their graceful termination when necessary.
- Resource Watching: The manager watches Kubernetes resources (e.g., Custom Resources, Pods, Services) to detect changes (such as create, update, delete events). It uses informers to efficiently keep track of these changes.
- Event Handling: When the manager detects changes to watched resources, it dispatches events to the relevant controllers. This allows controllers to react to changes in the cluster and perform reconciliation.
- Reconciliation Loop: The manager sets up and maintains a reconciliation loop for each controller. This loop periodically invokes the controller's reconciliation logic to ensure that the actual state of resources matches their desired state.
- Leader Election: It supports leader election mechanisms to ensure that only one instance of a controller is active at a time. This is important for high availability and to prevent multiple controllers from conflicting with each other.

By using the `controller-runtime` manager, developers can focus on writing the controller logic and delegate many of the operational and infrastructure concerns to the manager itself. This makes it easier to build robust, production-ready controllers for Kubernetes that can effectively manage resources and react to changes within the cluster.

### Setting up the controller with the manager in `contoller.go`:
```GO
// SetupWithManager sets up the controller with the Manager.
func (r *DruidReconciler) SetupWithManager(mgr ctrl.Manager) error {
    return ctrl.NewControllerManagedBy(mgr).
    For(&druidapi.Druid{}).
    Complete(r)
}
```
This is the method definition for setting up a controller with a Kubernetes manager using the "controller-runtime" framework. Let's break down what this code does:

-  `func (r *DruidReconciler) SetupWithManager(mgr ctrl.Manager) error { ... }`: This is a method of the DruidReconciler struct. It is used to configure and register the controller with a manager, which is an instance of the Kubernetes controller-runtime manager.
- `ctrl.NewControllerManagedBy(mgr)`: This line creates a new controller using the manager provided as an argument (mgr). The NewControllerManagedBy function is used to specify that this controller will be managed by the given manager.
- `.For(&druidapi.Druid{})`: This part of the code specifies the Kubernetes CustomResourceDefinition (CRD) type that the controller will watch and reconcile. In this case, it is set to kubedbcomv1alpha2.Druid{}, indicating that this controller is responsible for managing resources of this specific type.
- `.For(&druidapi.Druid{})`: This part of the code specifies the Kubernetes CustomResourceDefinition (CRD) type that the controller will watch and reconcile. In this case, it is set to kubedbcomv1alpha2.Druid{}, indicating that this controller is responsible for managing resources of this specific type.
- `.Complete(r)`: This method call completes the configuration of the controller, where r is an instance of the DruidReconciler. It associates your custom reconciler (DruidReconciler) with the controller. This means that when the manager detects changes in resources of type kubedbcomv1alpha2.Druid, it will call the reconciliation logic defined in your DruidReconciler.

In summary, the `SetupWithManager` method is used to set up and configure your controller to watch and reconcile resources of a specific type (in this case, `kubedbcomv1alpha2.Druid`) within your Kubernetes cluster. The controller will be managed by the provided manager, and its reconciliation logic will be invoked whenever there are changes to resources of the specified type.

### `main.go`:
1. A `controller-runtime` is initialized:
```GO
mgr, err := ctrl.NewManager(ctrl.GetConfigOrDie(), ctrl.Options{
		Scheme:                 scheme,
		Logger:                 logger,
		SyncPeriod:             &syncperiod,
		MetricsBindAddress:     metricsAddr,
		HealthProbeBindAddress: probeAddr,
		LeaderElection:         enableLeaderElection,
		LeaderElectionID:       "a7e00774.kubedb.com",
		// LeaderElectionReleaseOnCancel defines if the leader should step down voluntarily
		// when the Manager ends. This requires the binary to immediately end when the
		// Manager is stopped, otherwise, this setting is unsafe. Setting this significantly
		// speeds up voluntary leader transitions as the new leader don't have to wait
		// LeaseDuration time first.
		//
		// In the default scaffold provided, the program ends immediately after
		// the manager stops, so would be fine to enable this option. However,
		// if you are doing or is intended to do any operation such as perform cleanups
		// after the manager stops then its usage might be unsafe.
		// LeaderElectionReleaseOnCancel: true,
	})
```
2. 
```GO
if err = (&controller.DruidReconciler{
    KBClient: mgr.GetClient(),
    Scheme:   mgr.GetScheme(),
    Log:      mgr.GetLogger(),
    Client:   k8sClient,
}).SetupWithManager(mgr); err != nil {
    setupLog.Error(err, "unable to create controller", "controller", "Druid")
    os.Exit(1)
}
```
This code is setting up and configuring a Kubernetes controller of type DruidReconciler within a Go application using the "controller-runtime" framework. Let's break down what's happening in this code:

- `&controller.DruidReconciler{ ... }`: This code initializes an instance of the DruidReconciler controller by initializing necessary values i.e. `KBClient`, `Scheme` etc.
- `.SetupWithManager(mgr)`: This is a method `DruidReconciler` struct. After initializing a object of that struct, this method of the newly initialized struct is called. This method call sets up the DruidReconciler with the Kubernetes manager (mgr) by configuring the controller to watch and reconcile resources of a specific type, as explained in the previous response.

### How the reconciliation work for a custom resource?
- There is one manager for each CR and there can be multiple controllers in a k8s cluster.
- Whenever any event occurs for a CR, the `controller/Reconciler/reoncile()` function is triggered with the `NamespacedName` (`req ctrl.Request`) of that custom resource through the manager of that resource.
- The `func (r *DruidReconciler) Reconcile(ctx context.Context, req ctrl.Request) (ctrl.Result, error)` handles that event for that custom resource by retriving the details or current state about that resource from the cluster.

