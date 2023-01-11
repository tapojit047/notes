# Kubernetes Networking Abstraction

## StatefulSet
- Manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods.
- Like a Deployment, a StatefulSet manages Pods that are based on an identical container spec. Unlike a Deployment, a StatefulSet maintains a sticky identity for each of their Pods.

## Services:
- An abstract way to expose an application running on a set of Pods as a network service.

<!--- ![alt text](/home/notes/kubernetes/images/service1.png) -->


4 types:
- ClusterIP
- NodePort
- LoadBalancer
- ExternalName

### Headless service: 
- A headless service is a service with .spec.clusterIP: "None".
- In “StatefulSets”, if developers need to let the client decide which endpoint to use, headless is the appropriate type of service to deploy.

### LoadBalancer: 
- LoadBalancer service exposes services external to the cluster network.
