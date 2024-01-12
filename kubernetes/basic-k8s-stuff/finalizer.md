# Finalizer:
- A "finalizer" is a concept related to resource management and object lifecycle in the Kubernetes cluster. Finalizers are used to control the deletion of resources and allow for custom cleanup actions to be performed before a resource is removed from the cluster.
- When a resource (such as a Pod, Service, or Custom Resource Definition) is marked for deletion, Kubernetes will not immediately remove it from the cluster. Instead, it enters a deletion lifecycle, and finalizers can be defined to carry out specific actions before the resource is actually deleted. These actions can include cleaning up related resources, performing data backups, or other custom operations necessary to ensure that the resource's deletion is handled properly.
- Finalizers are defined as part of the metadata for Kubernetes resources, typically within the `metadata.finalizers` field. When a resource is marked for deletion, Kubernetes will process its finalizers in the order they are listed in the `metadata.finalizers` array. Once all the finalizers have completed their tasks, the resource is finally removed from the cluster.
- Here's a simplified example of how a finalizer might be defined in a Kubernetes Custom Resource:
```yaml
apiVersion: example.com/v1
kind: CustomResource
metadata:
  name: myresource
  finalizers:
    - my-finalizer.example.com
spec:
...
```
- In this example, when the "myresource" object is marked for deletion, Kubernetes will invoke the finalizer with the name "my-finalizer.example.com" to perform any necessary cleanup tasks.
- Finalizers are a crucial feature for ensuring the proper handling of resources in Kubernetes and are commonly used in custom controllers and operators to manage the lifecycle of custom resources effectively.

