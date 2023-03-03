# Notes on Cluster-API:
### Provider:
- In the context of the Kubernetes Cluster API, a provider refers to a component that implements and manages the underlying infrastructure resources that the cluster runs on, such as virtual machines, networks, and storage.
- Providers typically interact with the Kubernetes control plane through the Cluster API to provision and manage the lifecycle of these resources, including scaling them up or down, updating them, and deleting them when they are no longer needed.
- Examples of providers include cloud providers like AWS or GCP, bare metal providers like OpenStack, and on-premises virtualization platforms like VMware.
- 4 types of providers:
    - Core Provider
    - Infrastructure Provider
    - Bootstrapning Provider
    - Control Plane Provider

### Bootstarpping a Kubernetes cluster:
Bootstrapping a Kubernetes cluster refers to the process of setting up a new cluster from scratch. This involves configuring the infrastructure, installing and configuring Kubernetes components, and deploying any necessary applications and services.

Here are the general steps to bootstrap a Kubernetes cluster:
- Choose a cloud provider or on-premises infrastructure to host the cluster, and provision the necessary resources, such as virtual machines or physical servers.

- Install the Kubernetes control plane components, including etcd, kube-apiserver, kube-scheduler, and kube-controller-manager. This can be done using installation scripts or a tool like kubeadm.

- Install a container runtime, such as Docker or containerd, on each node in the cluster. This is necessary for deploying and running containerized applications on the cluster.

- Set up the networking layer for the cluster, including configuring the pod network, service network, and DNS service. This can be done using a network plugin, such as Calico or Flannel.

- Join the worker nodes to the cluster by running the necessary commands to connect to the control plane. This will allow the nodes to receive workloads and execute them on the cluster.

- Deploy any necessary applications and services to the cluster, such as monitoring and logging tools or the actual applications that will run on the cluster.

- Once the cluster is up and running, ensure it is properly secured by setting up RBAC (Role-Based Access Control), configuring network policies, and enabling TLS (Transport Layer Security) encryption.

Bootstrapping a Kubernetes cluster can be a complex process, but it is necessary to get a working cluster up and running. There are many resources available online that can provide detailed guidance on the process for specific cloud providers or on-premises infrastructure setups.
### Use Case of Cluster-API:
Cluster API is a versatile tool that can be used in a variety of use cases related to Kubernetes cluster management. Here are a few examples:
- **Multi-Cloud Management**: If you have a requirement to manage multiple Kubernetes clusters across multiple cloud providers, Cluster API can help you by providing a common way to create and manage those clusters. You can define the cluster specifications in a portable manner, regardless of the cloud provider, and use Cluster API providers to spin up clusters across multiple clouds.
- **On-Premises Infrastructure**: If you have on-premises infrastructure that you need to manage, Cluster API can help you manage your Kubernetes clusters on that infrastructure. You can use Cluster API to define the desired state of the cluster, and then use a provider to provision the necessary infrastructure, such as virtual machines or bare-metal servers, and deploy the cluster.
- **Dev/Test Environments**: Cluster API can be used to create and manage development and test environments for Kubernetes applications. You can define the cluster specification in a Git repository and use GitOps to manage the cluster lifecycle.

### What is infrastructure in Cluster-API?
- In the context of Cluster API, infrastructure refers to the underlying physical or virtual resources that are required to create and manage Kubernetes clusters. The infrastructure components typically include virtual machines or physical hosts, networking components, and storage components.
- Cluster API is designed to provide a declarative way to manage the infrastructure components required for Kubernetes clusters. It defines a set of custom resources that allow users to define the desired state of the infrastructure, and then uses controllers to reconcile the current state with the desired state.
- The infrastructure components required for a Kubernetes cluster can be provisioned and managed by different providers. A provider is responsible for managing the infrastructure resources for a specific platform, such as a cloud provider or an on-premises data center.
- Cluster API supports multiple providers, including AWS, Azure, Google Cloud Platform, and OpenStack, as well as providers for bare metal and on-premises infrastructure. By supporting multiple providers, Cluster API makes it easier to manage Kubernetes clusters across different infrastructure platforms and to migrate between them.
- Overall, infrastructure is a critical component of Cluster API, as it enables users to create and manage Kubernetes clusters in a portable and reproducible way, regardless of the underlying infrastructure platform.

### Bare Metal infrastructure:
- Bare metal infrastructure, also known as bare metal servers, refers to a physical server that is not running a hypervisor or any other form of virtualization. With bare metal infrastructure, the operating system and applications run directly on the hardware, without the overhead of a virtualization layer.
- Bare metal infrastructure can be used for a variety of purposes, such as running high-performance computing workloads, big data processing, and machine learning applications. It is particularly well-suited for applications that require low latency and high throughput, as it eliminates the overhead of a hypervisor or virtualization layer.
- Bare metal infrastructure can be provisioned and managed by a variety of tools, such as automation and orchestration platforms, like Kubernetes and OpenStack, or through cloud providers that offer bare metal instances.
- One of the main advantages of bare metal infrastructure is that it provides full control over the hardware and the operating system, allowing for fine-grained customization and optimization. This makes it particularly attractive for applications with specific hardware requirements or for organizations that require tight control over their infrastructure.
- However, bare metal infrastructure can be more expensive to maintain than virtualized infrastructure, as each server needs to be managed and maintained individually. Additionally, it may not be as flexible or scalable as virtualized infrastructure when it comes to changing the resource allocation or adding or removing servers.

### Management Cluster:
- A Kubernetes cluster that manages the lifecycle of Workload Clusters. A Management Cluster is also where one or more providers run, and where resources such as Machines are stored.
- In the context of the Cluster API, the management cluster is the Kubernetes cluster that is responsible for managing the lifecycle of other Kubernetes clusters. It's where you install and run the Cluster API controllers and other infrastructure components needed to manage the creation and management of Kubernetes clusters.
- The management cluster is also where you store the definitions of the custom resources used by the Cluster API, including the Machine resources that define the nodes in the target clusters. The management cluster acts as a hub for managing the entire lifecycle of a target cluster, from creation and initialization to scaling and deletion.
- In addition, one or more providers may run on the management cluster, depending on the needs of the target clusters. Providers are responsible for interacting with the underlying infrastructure (such as cloud providers, bare metal hosts, or virtualization platforms) to create and manage the nodes in the target cluster. By running the providers on the management cluster, you can more easily manage the entire lifecycle of the target cluster from a single location.

### Provider:
- In the context of the Cluster API, a provider is a software component that enables the creation and management of Kubernetes clusters on a specific infrastructure platform or environment. The provider is responsible for translating the declarative Cluster API objects, such as Machine and Cluster objects, into actions on the underlying infrastructure.
- Providers can support a wide range of infrastructure platforms, such as public cloud providers (e.g., AWS, Azure, GCP), on-premises data centers, bare-metal servers, and virtualization platforms (e.g., VMware, KVM, Hyper-V). Each provider implements a set of controllers that are responsible for interacting with the infrastructure platform to create, update, and delete resources, such as virtual machines or bare-metal servers.
- For example, a provider for a public cloud platform might use the cloud provider's APIs to create virtual machines, while a provider for a bare-metal infrastructure might use tools like IPMI to power on and off servers and configure them for use in a Kubernetes cluster.
- The Cluster API follows a pluggable architecture for providers, which means that new providers can be developed and added to the ecosystem, allowing users to create Kubernetes clusters on any infrastructure platform of their choice.

### Workload cluster:
- A workload cluster is a Kubernetes cluster that is created and managed using the Cluster API. It is a target cluster, which means that it is the cluster on which applications and services are deployed and run.
- The purpose of a workload cluster is to provide a reliable and scalable platform for running containerized applications and services. Workload clusters are typically created in response to specific business requirements, such as a need for a dedicated environment to run a specific application or workload.
- Using the Cluster API, a workload cluster can be created by defining the desired state of the cluster as a set of Kubernetes custom resources, such as Cluster, MachineDeployment, and MachineSet objects. These resources define the configuration and characteristics of the cluster, such as the number and types of nodes (workers and control plane), the networking and storage requirements, and other cluster-level settings.
- Once the desired state is defined, the Cluster API controllers running in the management cluster take care of the details of provisioning, configuring, and managing the workload cluster, using the provider-specific controllers to interact with the underlying infrastructure. This allows workload clusters to be created, scaled, and updated in a consistent and repeatable manner, with minimal manual intervention.

### Bootstrap Provider:
- a bootstrap provider is a software component that is responsible for bootstrapping the nodes in a Kubernetes cluster. Bootstrap providers work in conjunction with infrastructure-specific provider components to perform the necessary steps to prepare nodes for inclusion in the target cluster.
- The specific steps performed by the bootstrap provider depend on the infrastructure platform and the configuration of the target cluster. For example, a bootstrap provider for a cloud infrastructure platform might use cloud-init to configure the node, while a bootstrap provider for a bare-metal platform might use tools like iPXE or MAAS to provision and configure the node.
- By abstracting away the details of node bootstrapping, bootstrap providers make it easier to create and manage Kubernetes clusters in a consistent and repeatable way, regardless of the underlying infrastructure.

### Machine:
- In the context of the Cluster API, machines are individual nodes or virtual machines (VMs) that make up a Kubernetes cluster. The Cluster API is a Kubernetes subproject that provides a declarative way to provision and manage Kubernetes clusters using standard Kubernetes APIs.
- When using the Cluster API, machines are defined as custom resources in Kubernetes. Each machine resource represents a single node in the cluster and includes information such as the node's operating system, hardware specifications, and network configuration. The Cluster API can then use this information to provision, configure, and manage the machines that make up the cluster.
- By managing machines as Kubernetes resources, the Cluster API makes it easier to automate the process of creating and managing clusters. For example, you can use the Cluster API to create a set of machine templates that define the standard configuration for different types of nodes in the cluster, such as worker nodes or control plane nodes. You can then use these templates to create new nodes as needed, automatically scaling up or down the cluster in response to changing demand.

<!--- Bootstap provider watches Machines in "pending" state, generate BootstrapConfig.Status.DataSecretName and sets BootstrapConfig.Status.Ready = true --->

## Controllers:
- **Cluster Controller:**
  -  The Cluster Controller is one of the main controllers in the Cluster API of Kubernetes. It is responsible for managing the Cluster object, which is the top-level object in the Cluster API hierarchy, and represents the entire Kubernetes cluster.
  - The Cluster Controller is responsible for ensuring that the desired state of the Cluster object is achieved and maintained. To do this, it interacts with other controllers in the Cluster API, as well as the Kubernetes control plane, to create and manage the Kubernetes objects that make up the cluster.
  - The Cluster Controller performs several functions to manage the Cluster object. These include:
    - Creating and updating the control plane components
    - Managing the networking configuration
    - Managing the machine deployment
    - Managing the secrets and other resources
  - The Cluster Controller is an important component of the Cluster API, as it provides a centralized point of control for managing the entire Kubernetes cluster. By managing the Cluster object, the Cluster Controller ensures that the cluster is configured and maintained correctly, and that it meets the desired state defined by the user.
  
## Are machines and nodes same?
- No, machines and nodes are not the same in Kubernetes.
- A "node" in Kubernetes is a worker machine that runs one or more containers. It's the actual computer or virtual machine that hosts your applications and provides resources such as CPU, memory, and network connectivity.
- On the other hand, a "machine" in the context of the Cluster API is a Kubernetes custom resource that represents the desired state and metadata of a physical or virtual machine instance. A machine defines the characteristics of a node, such as the size of the machine, the operating system, and any additional software or configuration needed to run applications on the node.
- In summary, nodes are the actual computers or virtual machines that run your applications, while machines are Kubernetes resources that represent the desired state and metadata of those nodes.

## Do pods run inside machines?
- Technically, pods do not run directly inside machines, but rather inside nodes, which are managed by Kubernetes and run on top of the machines.
- To give some more detail: when a new node is added to a Kubernetes cluster, it typically runs a node agent or daemon that communicates with the cluster control plane to receive instructions on what workloads to run. The node agent then schedules and manages pods on the node. Each pod runs in its own network namespace and file system, and can contain one or more containers.
- So, while pods do not run directly inside the machines themselves, the machines provide the underlying resources (such as CPU, memory, and network connectivity) that the nodes and their pods rely on to run.

## Machine Pool:
- A machine pool is a collection of machines that share a common set of properties, such as the type of machine or the node label.

## ClusterCLass:
- ClusterClass is a Custom Resource Definition (CRD) that enables users to define a cluster topology that can be used by Cluster API to create and manage Kubernetes clusters. A ClusterClass defines a set of templates for various resources such as the Kubernetes control plane, worker nodes, load balancers, and other infrastructure components that are required for a cluster. A ClusterClass can be seen as a blueprint for a cluster that defines the infrastructure characteristics and requirements of the cluster, which can be used by Cluster API to deploy and manage clusters that conform to this specification.

# AWS-stuff:
## Fargate: 
- Fargate is a serverless compute engine for containers that enables developers to deploy and run containers without having to manage the underlying infrastructure. Fargate is part of the Amazon Elastic Container Service (ECS) and the Amazon Elastic Kubernetes Service (EKS) on AWS (Amazon Web Services) and allows users to run containers on a fully managed platform without the need to manage or provision servers.

## EKS:
- Amazon Elastic Kubernetes Service (EKS) is a managed Kubernetes service provided by Amazon Web Services (AWS). EKS allows you to easily deploy, manage, and scale Kubernetes clusters in the AWS cloud.
- With EKS, you can run Kubernetes applications on AWS without the need to manage the underlying infrastructure. EKS manages the deployment and scaling of the Kubernetes control plane, including the API server, etcd, and other components. EKS also integrates with other AWS services, such as Elastic Load Balancing, Elastic File System, and Identity and Access Management (IAM), to provide a seamless Kubernetes experience on AWS.

## VPC-CNI:
- VPC stands for Virtual Private Cloud. A Virtual Private Cloud (VPC) is a virtual network that is logically isolated from other networks in the cloud. VPCs allow you to create a private network within the cloud that is dedicated to your organization and can be customized to your specific networking needs.VPCs are an important component of cloud infrastructure that provide a secure and customizable private network for your cloud-based resources. They allow you to build and manage your own network infrastructure in the cloud while maintaining full control over security, performance, and availability.
- VPC CNI (Container Network Interface) is a plugin that provides networking support for Kubernetes pods running on Amazon Web Services (AWS) Elastic Kubernetes Service (EKS). It enables Kubernetes pods to communicate with each other and with other AWS resources by assigning unique IP addresses to each pod and configuring the necessary network routes.

## Amazon VPC:
- Amazon VPC (Virtual Private Cloud) is a service provided by Amazon Web Services (AWS) that allows you to create a private, isolated section of the AWS Cloud where you can launch resources such as EC2 instances, databases, and other AWS services.
- VPC provides you with complete control over your virtual networking environment, including selection of IP address ranges, creation of subnets, and configuration of route tables and network gateways. With VPC, you can also create a secure and scalable environment for your applications and workloads.
- By default, VPCs are isolated from each other and the internet. However, you can also configure your VPC to connect to the internet, to other VPCs, and to your own data center using AWS Direct Connect or VPN. You can also use security groups and network access control lists (ACLs) to control inbound and outbound traffic to your resources.
- Overall, Amazon VPC is a powerful service that provides a flexible and secure way to launch resources in the AWS Cloud, while also giving you complete control over your virtual networking environment.

## VPC:
- A virtual private cloud (VPC) is a private network environment in the cloud, similar to a traditional network that you would have in an on-premises data center. It allows you to create a virtual network within a cloud service provider's infrastructure where you can launch resources such as virtual machines (VMs), databases, and other services.
- With a VPC, you can define and control the IP addresses and subnets used within your virtual network, and also configure routing and security settings to control inbound and outbound traffic to and from your resources.
- VPCs are commonly used in cloud computing to provide a secure and isolated environment for running applications, particularly those that require specific network configurations or security requirements. By using a VPC, you can separate your resources from other customers' resources and also from the public internet, providing an additional layer of security.
- VPCs are offered by many cloud service providers, including Amazon Web Services (AWS), Microsoft Azure, and Google Cloud Platform (GCP). Each provider offers their own unique features and capabilities for VPCs, but the basic idea remains the same: to provide a secure and isolated network environment within the cloud.

## Subnets:
- Subnets are subdivisions of a larger network or IP address range. In a network, a subnet is created by dividing the IP address space into smaller, more manageable sections. This allows for better organization and management of network resources.
- Subnets are often used to isolate different types of network traffic or to group resources together based on their function. For example, in a virtual private cloud (VPC), subnets can be used to create separate sections of the VPC for different types of resources, such as web servers, application servers, and databases. Each subnet can have its own routing tables and security policies, allowing for fine-grained control over network traffic.
- Subnets are identified by their network prefix, which is a portion of the IP address that identifies the subnet. The network prefix is usually written in CIDR notation, which consists of the IP address followed by a slash (/) and the number of bits used for the network prefix. For example, a subnet with a network prefix of 10.0.0.0/24 would include all IP addresses from 10.0.0.0 to 10.0.0.255.
- A subnet is a range of IP addresses in your VPC. A subnet must reside in a single Availability Zone. After you add subnets, you can deploy AWS resources in your VPC.
- Subnets are a fundamental building block of modern networks and are used extensively in both on-premises and cloud-based environments.

## IP addressing:
- IP addressing is a method used to uniquely identify devices on a network using a series of numbers. An IP address is a numeric label assigned to each device on a network that uses the Internet Protocol (IP) for communication. The IP address allows devices to communicate with each other over the network and enables the transmission of data between them.
- You can assign IPv4 addresses and IPv6 addresses to your VPCs and subnets

## Routing:
- Routing is the process of determining how network traffic should be directed from one device to another across a network. Routing is a fundamental concept in networking and is used to ensure that data packets are sent to the correct destination.
- When a device sends a data packet across a network, it includes the IP address of the destination device. The network uses this information to determine the most efficient path for the packet to reach its destination. This involves looking at the routing table, which is a list of destinations and their associated network paths.
- Each device on a network has a routing table that contains information about the network topology and the available routes to other devices. When a packet arrives at a device, the device consults its routing table to determine the best path for the packet to take to reach its destination.
- There are several routing protocols that are used to exchange routing information between devices on a network. These protocols allow devices to dynamically update their routing tables in response to changes in the network topology, such as the addition or removal of devices or changes in network link status.
- In cloud computing environments, such as Amazon Web Services (AWS), routing plays a critical role in managing network traffic between resources in a virtual private cloud (VPC). AWS provides a variety of routing options, including static and dynamic routing, to help you control how traffic flows between resources in your VPC. Understanding routing is essential for designing and managing network infrastructure in the cloud.

## Route Table:
- A route table is a table of rules that is used by a network device to determine the path that network traffic should take when it is sent to a particular destination. The route table contains a list of destination networks and their associated next hops, which are the network devices that traffic should be sent to in order to reach those destinations.
- In a typical network, each device has a route table that is used to determine how traffic should be routed between different subnets or networks. When a device receives a packet of data, it looks up the destination IP address in its route table to determine the next hop for the packet. The packet is then sent to that next hop, which in turn repeats the process until the packet reaches its final destination.
- In a virtual private cloud (VPC) in Amazon Web Services (AWS), each subnet has its own route table, and the VPC has a main route table that is associated with the VPC itself. The route tables in a VPC are used to control how traffic flows between subnets and between the VPC and other networks.
- AWS route tables can be configured with a variety of rules, including static routes that are manually configured by the network administrator, and dynamic routes that are learned automatically through routing protocols such as Border Gateway Protocol (BGP). By configuring route tables in a VPC, you can control how traffic flows between different resources in your VPC, and between your VPC and other networks.

## Gateways:
- A gateway is a device that connects two or more networks together, often acting as a bridge between different types of networks. Gateways are used to enable communication between networks that use different protocols or technologies, such as connecting a local area network (LAN) to the internet.
- In cloud computing environments, gateways are often used to provide connectivity between a virtual private cloud (VPC) and other networks or services. For example, an internet gateway can be used to provide access to the internet from a VPC, while a virtual private gateway can be used to establish a secure connection between a VPC and an on-premises network.


## Endpoints:
- Endpoints are devices or applications that send or receive data over a network. Endpoints can include a wide variety of devices, such as computers, smartphones, servers, and IoT devices, as well as applications and services that communicate over the network.
- Endpoints are the source and destination of network traffic, and they can be located anywhere in the network. In a typical network architecture, endpoints are connected to switches and routers, which are responsible for forwarding data packets between endpoints and between different networks.
- Endpoints can communicate with each other using a variety of protocols.

## VPC Endpoints:
- A VPC endpoint is a service provided by Amazon Web Services (AWS) that enables you to connect your virtual private cloud (VPC) to AWS services and endpoints without requiring internet access. With a VPC endpoint, you can privately access AWS services such as Amazon S3 and DynamoDB from within your VPC, without exposing your data to the public internet.

## Peering Connections:
- Peering connections are a feature of Amazon Web Services (AWS) that allow two or more virtual private clouds (VPCs) to communicate with each other using private IP addresses. Peering connections enable you to create a private network connection between VPCs located in the same or different AWS accounts, without requiring internet access.
- Peering connections are established between two VPCs by creating a peering connection request, which must be accepted by the owner of the target VPC. Once the peering connection is established, the VPCs can communicate with each other using private IP addresses, as if they were part of the same network.
- Peering connections provide several benefits for network architecture in AWS, including:
  - Simplified network architecture: Peering connections enable you to create a flat and scalable network architecture, without requiring complex routing or additional network devices.
  - Reduced network costs: Peering connections enable you to exchange data between VPCs without incurring data transfer charges, as long as the VPCs are located in the same AWS region.
  - Improved network performance: Peering connections provide low-latency and high-bandwidth connectivity between VPCs, which can improve application performance and reduce latency.
  - Enhanced security: Peering connections enable you to establish private and secure network connections between VPCs, without exposing your data to the public internet.
- However, there are some limitations to peering connections that you should be aware of, such as:
  - Limited scalability: Peering connections are limited to a single VPC and cannot be used to create mesh networks or connect more than two VPCs together.
  - Limited transitive routing: Peering connections do not support transitive routing, which means that you cannot use a peering connection to route traffic between VPCs that are not directly connected.
- Overall, peering connections are a powerful tool for building private and secure network connections between VPCs in AWS. They provide a simple, scalable, and cost-effective way to connect VPCs and enable you to take full advantage of the flexibility and scalability of the AWS cloud.

## Traffic Monitoring:
- Traffic mirroring is a feature provided by Amazon Web Services (AWS) that enables you to monitor network traffic within your Amazon Virtual Private Cloud (VPC) by copying network traffic from an elastic network interface (ENI) attached to an Amazon Elastic Compute Cloud (EC2) instance and sending it to a destination that you specify, such as an Amazon S3 bucket or an Amazon Kinesis Data Firehose stream.
- Traffic mirroring is a powerful tool for monitoring network traffic within your VPC and gaining visibility into network behavior. It provides a range of benefits for network security, performance, and compliance, and can be used for a variety of use cases in AWS.

## Transit gateways:
- Transit Gateways are a feature of Amazon Web Services (AWS) that provide a centralized hub for connecting multiple virtual private clouds (VPCs) and on-premises networks. Transit Gateways simplify network architecture and reduce the operational complexity of managing multiple VPCs and VPN connections by enabling you to connect them through a single gateway.
- Transit Gateways provide several benefits for network architecture in AWS, including:
  - Simplified network architecture: Transit Gateways enable you to create a hub-and-spoke network architecture that simplifies network design and reduces the need for complex routing and multiple VPN connections.
  - Scalability: Transit Gateways support the connection of up to 5,000 VPCs and on-premises networks, enabling you to scale your network architecture to meet your business needs.
  - Centralized management: Transit Gateways provide a centralized management console that simplifies the management of network resources and enables you to view network traffic and usage across multiple VPCs.
  - Enhanced security: Transit Gateways support network segmentation and isolation, enabling you to create security boundaries between VPCs and on-premises networks.
- To use Transit Gateways, you must create a Transit Gateway resource in your AWS account and attach VPCs and on-premises networks to the Transit Gateway. Once attached, the VPCs and on-premises networks can communicate with each other using private IP addresses, and you can use Transit Gateway Route Tables to control the routing of traffic between them.
- Overall, Transit Gateways are a powerful tool for simplifying network architecture in AWS and enabling you to connect multiple VPCs and on-premises networks through a single gateway. They provide scalability, centralization, and enhanced security features that can help you improve the performance and security of your network infrastructure in AWS.

## VPC Flow Logs:
- VPC Flow Logs is a feature provided by Amazon Web Services (AWS) that enables you to capture and log information about the IP traffic going to and from network interfaces in your Amazon Virtual Private Cloud (VPC). VPC Flow Logs provide detailed information about the network traffic in your VPC, including the source and destination IP addresses, protocols, ports, and the number of bytes and packets transmitted.

## VPN Connections:
- VPN (Virtual Private Network) is a technology that allows you to establish a secure, encrypted connection between two networks over the internet. VPN connections are commonly used by organizations to provide secure access to their corporate network for remote workers or to connect multiple locations of a business.
- When you connect to a VPN, your device creates an encrypted tunnel between itself and the VPN server, which can be located anywhere in the world. All the data sent between your device and the VPN server is encrypted, ensuring that it cannot be intercepted or read by anyone who might be monitoring your internet connection.

