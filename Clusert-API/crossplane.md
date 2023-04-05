# Crossplane:
- Crossplane is an open-source Kubernetes add-on that enables you to manage infrastructure and services as code. It is a control plane that extends the Kubernetes API by providing a set of custom resources that represent infrastructure resources such as databases, message queues, cloud storage, and others.
- Crossplane connects your Kubernetes cluster to external, non-Kubernetes resources, and allows platform teams to build custom Kubernetes APIs to consume those resources.
- With Crossplane, you can define infrastructure resources as Kubernetes objects, and use Kubernetes declarative syntax to manage their lifecycle, just like you would manage a Kubernetes application. Crossplane integrates with various cloud providers and platforms such as Amazon Web Services (AWS), Google Cloud Platform (GCP), Microsoft Azure, and more, allowing you to manage your infrastructure and services across different cloud providers in a unified way.
- Crossplane also provides a framework for building custom infrastructure resources called "Providers" which are responsible for managing a particular infrastructure service or resource. This enables you to extend Crossplane's capabilities and integrate it with your own custom infrastructure resources.

# Composite Resources:
- In Crossplane, a composite resource is a single resource that represents a collection of related resources. It is created by combining multiple simpler resources using Crossplane's composition capability.

# Composite Resource Definitions:
- A composite resource definition (XRD) in Crossplane is similar to a Kubernetes Custom Resource Definition (CRD), but it's used to define a composite resource that is made up of other simpler resources. An XRD specifies the composition of resources, including the dependencies between them, and can be used to create a composite resource.
- For example, let's say you want to deploy a three-tier web application on a Kubernetes cluster, consisting of a front-end web server, a middle-tier application server, and a back-end database server. You could create a composite resource definition that defines how to compose these resources into a single, more complex resource. The XRD would specify the dependencies between the resources, such as that the web server depends on the application server, and that the application server depends on the database server.
- Once you have created an XRD, you can use it to create composite resources using Crossplane's declarative API. The XRD serves as a blueprint for the composite resource, allowing you to easily provision and manage complex applications and workloads. By defining a composite resource using an XRD, you can reduce the time and effort required for manual configuration and management, while also ensuring consistency and reliability across your application or workload.

# Steps of creating peering between two virtual networks using Crossplane:
- Install crossplane
- Install Upbound/Provider-Azure (https://marketplace.upbound.io/providers/upbound/provider-azure/v0.30.0)
- Create peering connection from both sides, both virtual networks. An example yaml for creating two peering connection between new-cluster5(DB-cluster) and aksctl-cluster(Application-Cluster) is given:
```yaml
apiVersion: network.azure.upbound.io/v1beta1
kind: VirtualNetworkPeering
metadata:
  name: link1
spec:
  forProvider:
    allowForwardedTraffic: true
    virtualNetworkName: new-cluster5-vnet
    resourceGroupName: new-cluster5
    remoteVirtualNetworkId: /subscriptions/1bfc9f66-316d-433e-b13d-c55589f642ca/resourceGroups/aksctl-resource-group/providers/Microsoft.Network/virtualNetworks/aksctl-cluster-vnet
---
apiVersion: network.azure.upbound.io/v1beta1
kind: VirtualNetworkPeering
metadata:
  name: link2
spec:
  forProvider:
    allowForwardedTraffic: true
    virtualNetworkName: aksctl-cluster-vnet
    resourceGroupName: aksctl-resource-group
    remoteVirtualNetworkId: /subscriptions/1bfc9f66-316d-433e-b13d-c55589f642ca/resourceGroups/new-cluster5/providers/Microsoft.Network/virtualNetworks/new-cluster5-vnet
```
- You can get the ``remoteVirtualNetworkId`` from the ``Properties`` option of the ``Virtual network``.