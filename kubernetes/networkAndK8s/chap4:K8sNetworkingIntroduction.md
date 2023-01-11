## Kubernetes Networking intro
- Kubernetes relies on the CNI project to comply with the following requirements:

  - All containers must communicate with each other without NAT (Network Address Translator).
  - Nodes can communicate with containers without NAT.
  - A container’s IP address is the same as those outside the container that
  it sees itself as.
- Kubernetes users typically do not create pods directly. Instead, users create a
high-level workload, such as a deployment, which manages pods according
to some intended spec. 
- There are also third-party workload types, in  the form of custom resource definitions (CRDs).
- Pods themselves are ephemeral, meaning they are deleted and replaced with
new versions of themselves.
- A pod has a unique IP address, which is shared by all containers in the pod.
The primary motivation behind giving every pod an IP address is to remove
constraints around port numbers. In Linux, only one program can listen on a
given address, port, and protocol. If pods did not have unique IP addresses,
then two pods on a node could contend for the same port (such as two web
servers, both trying to listen on port 80).
- Every Kubernetes node runs a component called the Kubelet, which manages
pods on the node. The networking functionality in the Kubelet comes fromAPI interactions with a CNI plugin on the node. The CNI plugin is what
manages pod IP addresses and individual container network provisioning.The CNI defines a standard interface to manage a container’s
network. Kubernetes does not ship with a default CNI plugin, which means that in a standard
installation of Kubernetes, pods cannot use the network.