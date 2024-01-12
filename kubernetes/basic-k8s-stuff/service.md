# Service:
### What is service and why we need it?
1. **Pod IP not stable:**
   - Each pod has its own IP Address. But pods are `Ephemeral`. 
   - When a pod dies, the IP address of that pod gets changed.
   - So depending on pod's ip address for contacting to the pod is not reliable.
   - As a result, the pod is exposed through a service which has a stable IP address. The set of Pods targeted by a Service is usually determined by a selector that you define.
2. **Loadbalancing**:
    - There can be multiple replica of a pod.
    - For any incoming traffic distribution and one IP address for accessing those replicas are needed.
    - That's why service's act as Loadbalancer to distribute the traffic among the pods.
3. **Loose coupling**
4. **Within & outside cluster**:
   - Services can be used to expose the pods outside the cluster.

### The default service for type is ClusterIP.
## ClusterIP:
- If in the YAML, no type then the default is Service type is ClusterIP.
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - protocol: TCP
      port: 3200
      targetPort: 3000
```
![Screenshot from 2023-11-02 16-32-23.png](..%2F..%2Fimages%2FScreenshot%20from%202023-11-02%2016-32-23.png)

1. The set of Pods targeted by a Service is usually determined by a selector that you define. For the YAML above, pods with label `app.kubernetes.io/name: MyApp` will be selected.
2. After determining the pods, the ports are used to forward the traffic to the appropriate application. Each application running in a container usually listens to a specific port of the machine/pod. So, service have to forward the traffic to the appropriate port, where the application is listening to. As a result `port` and `servicePort` comes into play.
3. `ServicePort`: 
  - "port: 3200" in the YAML specifies servicePort. 
  - To access those pods, the application forwards to servicePort of the service that maps to the desired applications port.
  - The service forwards the traffic to the `targetPort: 3000` which associated with the `port: 3200`
  - What the service basically do is, it forwards the incoming traffic at its port `3200` to pod's port `3000`  
  - Service port is arbitary. We can give any port we want to.
4. `targetPort`:
   - `targetPort` is the port of the pod/machine where the desired application's container listens to. In this case it is `3000`
   - TargetPor must match the port, the container is listening to.

### Single Service Handling multiple endpoint request:
![Screenshot from 2023-11-02 16-51-52.png](..%2F..%2Fimages%2FScreenshot%20from%202023-11-02%2016-51-52.png)
- A service can handle multiple endpoint request.
- In this case, the service has two `servicePort` open for forwarding into two container running inside each replicas of pod.
- In this case in the YAML, it is a must to name the ports. Like in the example:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: mongodb-service
spec:
  selector:
    app: mongodb
  ports:
    - name: mongodb  
      protocol: TCP
      port: 27017
      targetPort: 27017
    - name: mongodb-exporter
      protocol: TCP
      port: 9216
      targetPort: 9216
```
- Also notice that in these cases, `servicePort` = `targetPort`, which is usually followed.

## Headless Service:
In Kubernetes, a "headless service" is a type of service that does not allocate a cluster IP and does not perform load balancing for incoming network traffic. Instead, it's used for service discovery and DNS-based routing, allowing pods to discover the individual IP addresses of the backend pods associated with the service. Here are some key characteristics and use cases for headless services:
- **Cluster IP**: A typical Kubernetes service assigns a cluster IP, and all requests to that service are directed to one of the pods behind the service, distributing the traffic among the available pods. This behavior is suitable for most services, but in some cases, you may need a different approach.
- **No Cluster IP**: A headless service, on the other hand, is created with clusterIP: None. This means it does not have a stable cluster IP. As a result, no load balancing is performed. Instead, it exposes DNS records for the pods associated with the service.
- **DNS-Based Service Discovery**: Even though it lacks a cluster IP, Kubernetes creates DNS records for a headless service. Each DNS record corresponds to an individual pod behind the service. This makes it possible for applications to discover and communicate directly with specific pods by using their DNS names.
- **StatefulSets**: Headless services are frequently used in conjunction with StatefulSets, which are a type of workload in Kubernetes. StatefulSets require stable network identities for pods, as they often represent stateful applications. The headless service helps maintain these stable identities by allowing direct DNS-based communication to specific pods.

_**Use Cases for Headless Services:**_
- Stateful Applications: Stateful applications, such as databases, message brokers, and distributed systems, often require direct pod-to-pod communication and stable network identities. Headless services are a good fit for these use cases.
- Database Clusters: When deploying a database cluster with multiple pods, each pod may need to communicate directly with others. A headless service facilitates this direct communication.
- Custom DNS Resolution: If you need to implement custom DNS resolution within your application, headless services provide a straightforward way to do this.

In summary, a headless service is a Kubernetes service without a stable cluster IP, primarily used in scenarios where direct pod-to-pod communication, custom DNS resolution, or stable network identities are required. It's a valuable tool when working with stateful and distributed applications in Kubernetes.

### NodePort Service:
![Screenshot from 2023-11-03 11-26-55.png](..%2F..%2Fimages%2FScreenshot%20from%202023-11-03%2011-26-55.png)

- NodePort is service that is accessible to a static port in each worker node in the cluster.
- ClusterIP only accessible within the cluster. But external traffic has access to fixed port or NodePort on each worker node.
- Here ClusterIP service is automatically created which forwards the traffic from service port to targetPort.
- Basically NodePort type is an extension of ClusterIP type.

- A NodePort is a type of service in Kubernetes that allows you to expose a service on a specific port of each node in the cluster. This means that the service can be accessed from outside the cluster by connecting to any node's IP address on the specified port. NodePort is one of the ways to make services in a Kubernetes cluster accessible externally.
- Here's how NodePort works:
  - When you create a NodePort service, Kubernetes assigns a specific port from a predefined range (usually in the range 30000-32767) on each node in the cluster.
  - The service listens on this NodePort on every node.
  - When traffic is directed to any node's IP address on the assigned NodePort, the service forwards the traffic to the pods associated with that service.
- Consideration and limitation:
  - NodePort services are not typically used for securing or load balancing production services. In a production environment, you'd often use an external load balancer or ingress controllers for better control, security, and routing.


### LoadBalancer:
![Screenshot from 2023-11-03 11-37-01.png](..%2F..%2Fimages%2FScreenshot%20from%202023-11-03%2011-37-01.png)
- LoadBalancer Service  is an extension of NodePort Service type, which is an extension of ClusterIP type.
- For solving the limitation of NodePort, LoadBalancer is introduced where instead of exposing through a port of the node, the clusterIP service is exposed through an external LoadBalancer.
- `K8S` does not provide LoadBalancer functionality. It uses cloud providers LoadBalancer.
- When LoadBalancer service type is created, NodePort and ClusterIP Service are created automatically, where the LoadBalancer routes the traffic to. 