# API Group:
In Kubernetes, an API Group is a mechanism for logically grouping related resources together in the Kubernetes API. API groups allow you to organize and extend the Kubernetes API by introducing new resources, often referred to as "Custom Resources," and associated controllers for managing those resources. API groups are primarily used for creating custom resources and operators, which are extensions of Kubernetes.

Here are some key points about API Groups in Kubernetes:
- **Core API Group**: The core Kubernetes API group is often referred to as the "core" or "v1" group, and it includes built-in resources such as Pods, Services, Deployments, ConfigMaps, and more. These resources are available by default in a Kubernetes cluster.
- **Custom Resources**: You can extend Kubernetes by defining your custom resources and associated controllers. Custom resources are typically defined in a separate API group. This separation allows you to maintain your resources independently of the core Kubernetes resources.
- **API Group Versions**: Within an API group, there can be multiple versions of resources. For example, you might have version 1 of your custom resource in one API group and version 2 in another. This versioning allows for changes and updates to the resource definitions over time while preserving backward compatibility.
- **Group-Scoped Paths**: API groups are accessed via group-scoped paths in the Kubernetes API server. For example, the core API group uses paths like /api/v1, while a custom API group might use paths like /apis/mygroup.example.com/v1alpha1. The API server routes requests to the appropriate API group based on the path.
- **API Group Names**: API groups are identified by their names. The name of an API group is usually a DNS subdomain, and it must follow the DNS label naming conventions. For example, "extensions" and "apps" are commonly used names for API groups that contain resources related to deployments and replica sets.
- **CRDs (Custom Resource Definitions)**: To define custom resources in an API group, you typically create Custom Resource Definitions (CRDs). CRDs specify the structure, validation rules, and behaviors of your custom resources. These definitions are stored in the cluster and are used to validate and process custom resource objects.
- **Controllers**: When you create custom resources, you often need controllers to watch, reconcile, and manage those resources. These controllers are responsible for ensuring that the state of the cluster matches the desired state as specified in the custom resources.

API Groups are a fundamental concept in Kubernetes extension and customization, allowing you to build and manage resources tailored to your specific applications and workloads. They enable you to leverage the Kubernetes platform's powerful management capabilities while introducing your own domain-specific resources and controllers.

# Kind:

- API Group-Version: In Kubernetes, an API Group-Version represents a specific version of a set of resources within an API group. API Group-Versions are used to organize related resources and their definitions. Each API Group-Version has its own endpoint in the Kubernetes API server and is associated with a specific version of the resources.
- Kind: Each API group-version contains one or more API types, which we call Kinds. Kinds are the types of resources defined within an API Group-Version. For example, "Pod," "Service," "Deployment," and "ConfigMap" are all Kinds within the core Kubernetes API Group-Version.

_So, for identifying each resource in Kubernetes the `Group-Version-Kind (GVK)` concept is used._

- In the `apiVersion` field, Group = `apps`, version = `v1` and Kind = `Deployment`
- In Kubernetes API Server, this resource is registered in this path `apis/apps/v1/deployment` 

```yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

# Resource:
-  A resource is simply a use of a Kind in the API. Often, there’s a one-to-one mapping between Kinds and resources. For instance, the `pods` resource corresponds to the `Pod` Kind.

## Resource Vs Kind:
**Resource**:
- In Kubernetes, a "Resource" refers to a specific type of object that can be created, managed, and manipulated within a Kubernetes cluster.
- Resources represent different components or aspects of the system, such as Pods, Services, Deployments, ConfigMaps, and more. These are built-in resources that are part of the core Kubernetes API.
- Resources have specific fields, behaviors, and characteristics defined by their resource schema. For example, Pods have fields for containers, Services define networking rules, and Deployments manage replica sets and scaling.

**Kind**:
- "Kind" is a subfield within a Kubernetes object's metadata that specifies the type of the object. The "Kind" field indicates which resource or object type an instance belongs to.
- The "Kind" is used to categorize objects into different resource types. It is one of the key fields in an object's metadata, along with "apiVersion," "metadata," and "spec."
- The "Kind" is crucial for the Kubernetes API server and controllers to understand how to interpret and handle an object. It tells Kubernetes which type of resource the object represents.
- "Kind" is a way to differentiate objects, but it doesn't define the structure or behavior of the resource itself. The resource's structure and behavior are defined by its resource schema.

In summary, the "Kind" is a categorization field within the metadata of a Kubernetes object, indicating the type of resource the object represents, while the "Resource" refers to the specific type of object with its defined schema and behaviors within the Kubernetes ecosystem. The "Kind" helps Kubernetes determine how to process and manage an object, while the "Resource" defines the object's attributes, configuration, and interactions with other components in the cluster.