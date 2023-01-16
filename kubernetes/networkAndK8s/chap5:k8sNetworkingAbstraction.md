# Kubernetes Networking Abstraction

## StatefulSet
- Manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods.
- Like a Deployment, a StatefulSet manages Pods that are based on an identical container spec. Unlike a Deployment, a StatefulSet maintains a sticky identity for each of their Pods.

## Services:
- An abstract way to expose an application running on a set of Pods as a network service.
-You then create Kubernetes Service objects (svc) that sit in front of your Pods to provide stable and reliable networking. In this model, everything talks to Services instead of directly to Pods.


![alt text](https://github.com/tapojit047/notes/blob/master/kubernetes/images/service1.png)
![alt text](https://github.com/tapojit047/notes/blob/master/kubernetes/images/service2.png)
![alt text](https://github.com/tapojit047/notes/blob/master/kubernetes/images/service3.png)

4 types:
- ClusterIP
- NodePort
- LoadBalancer
- ExternalName

## NodePort:
- For accessing a pod using NodePort service:

``
 <node-ip>:nodePort
``

Example:

``
172.18.0.2:31000/books
``

- For accessing pod by forwarding port of service:

``
kubectl port-forward svc/<service-name> <localhost-port>:<port-of-service>
``

Example:

``
kubectl port-forward svc/my-service 8000:80
``
## Endpoints:
- Behind the scenes, every Service has an associated Endpoints object that’s a list of all the active healthy Pods that match the Service’s selector.

## Endpoint Slice:
- Assume you’ve got a Service sitting in front of lots and lots of Pods. The Service has an Endpoints object that holds the IP and port of every one of those lots and lots of Pods. This Endpoints object gets sent over the network to every node in the cluster and is used to create local networking rules etc.
- The problem is…. every time you add or remove a Pod from behind the Service, the entire Endpoints object gets updated, sent across the network, and consumed by every node.
- The principle behind Endpoint Slices is pretty simple. Take that single large monolithic Endpoints object, and slice it up into smaller more consumable slices.
- each Endpoint Slice will hold 100 actual endpoints 

### Headless service: 
- A headless service is a service with .spec.clusterIP: "None".
- In “StatefulSets”, if developers need to let the client decide which endpoint to use, headless is the appropriate type of service to deploy.

### LoadBalancer: 
- LoadBalancer service exposes services external to the cluster network.

## Ingress:
- An API object that manages external access to the services in a cluster, typically HTTP.
- Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster. Traffic routing is controlled by rules defined on the Ingress resource.
- An Ingress controller is responsible for fulfilling the Ingress.
- To manage traffic in a cluster with ingress, there are two components required: the controller and rules. The controller manages ingress pods, and the rules  deployed define how the traffic is routed.
- Ingresses have a “default backend” where requests are routed if no rule matches. 
- When a request matches multiple paths, the most specific match is chosen.

## Service Mesh:
- A service mesh is an API-driven infrastructure layer  for handling service-to-service communication.