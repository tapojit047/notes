## Containers Network
### Container
- Containers are a way to package software in a format that can be easily run on any computer, regardless of the operating system or environment. They allow developers to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package.
- Containers are isolated from each other and the host system, which means that they can be run on any computer and have no conflicts with other applications or the operating system itself. This makes them an ideal solution for running and deploying applications in a consistent and predictable manner.
- Containers are often used in conjunction with container orchestration tools, such as Kubernetes, to manage and deploy a large number of containers at once.

### Hypervisor
- A hypervisor, also called a virtual machine manager, is a software program that allows multiple operating systems to share a single hardware host. It creates virtual environments, called virtual machines, on which you can run different operating systems and their applications.
- The hypervisor acts as an intermediary between the physical hardware and the virtual machines, allowing each virtual machine to share the hardware resources of the host. This enables you to run multiple operating systems and their applications on a single physical machine, which can be useful for testing and development, or for running multiple applications that have different hardware or software requirements.

### Kernel:
- The kernel is the central part of an operating system that controls all the other parts of the system. It is responsible for managing the hardware and software resources of the computer, and for allowing different programs and users to share those resources.
- The kernel acts as the intermediary between the hardware and the software, and is responsible for tasks such as memory management, task scheduling, and input/output (I/O) operations. It also provides a set of services and interfaces that can be used by other parts of the operating system and by applications.
- In general, the kernel is the most important part of an operating system, and is responsible for making the hardware and software work together in a seamless and efficient manner.

### Docker:
- Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package.

- When the application is run, it runs inside a container. This container is an isolated environment that includes everything the application needs to run, including the application code and its dependencies. This makes it easier to run the application because the developer does not have to worry about installing all of the required libraries and dependencies on the host machine.

- Docker also makes it easier to deploy applications, because the developer can simply ship the container to the deployment environment, rather than having to worry about setting up the environment and installing all of the necessary dependencies.

- Overall, Docker is a tool that helps developers build, ship, and run applications more easily by using containers.

### Container Daemon:
- The containerd daemon is a background process that is responsible for managing the lifecycle of containers. It is an open-source component of the container ecosystem, and it is designed to be lightweight and efficient.

### OCI:
- OCI stands for the Open Container Initiative. It is a standards body that is responsible for defining standards for container runtime and image format.
- The goal of the OCI is to create open standards for containers that can be used by any container runtime environment, such as Docker or containerd. By defining these standards, the OCI helps to ensure that containers are portable and can be used across a wide range of environments.

### Container Primitives:
- Each of our containers has Linux primitives known as control groups and namespaces.

### Cgroup:
- cgroups (short for "control groups") is a Linux kernel feature that allows administrators to limit, prioritize, and distribute resources such as CPU, memory, and I/O bandwidth among groups of processes.

- cgroups work by creating a hierarchy of groups, and each group is assigned a set of resource limits. Processes can then be added to these groups, and they will be restricted to the resources that have been allocated to the group. This makes it easier for administrators to ensure that critical processes have access to the resources they need, while also preventing less important processes from using too many resources.

- cgroups are often used in conjunction with container runtime environments, such as Docker, to help manage the resources that are available to containers. By using cgroups, administrators can ensure that each container is only able to use a specific amount of resources, which can help to improve the overall performance and stability of the system.
- A cgroup controls how much of a resource a container can use, while namespaces  control what processes inside the container can see.

### Namespaces:
- Namespaces are features of the Linux kernel that isolate and virtualize system
resources of a collection of processes.

### Container Networking Modes:
- **None**: Use this mode when the container does not need network access.
- **Bridge**: In bridge networking, the container runs in a private network internal to
the host. Communication with other containers in the network is open.Bridge mode is the
default mode of networking when the --net option is not specified.
- Host: In host networking, the container shares the same IP address and the
network namespace as that of the host.
- **Macvlan**
- **Overlay**: Overlay allows for the extension of the same network across hosts in a
container cluster.
- **Custom**

### Docker Networking Model:
Three components:

- **Sandbox**: In Docker networking, a sandbox is a lightweight container network namespace that holds the network configuration for a container. It is used to isolate the network stack of a container from other containers and the host system.
- **Endpoint**: An endpoint is a connection point for a container to a network. Each container can have one or more endpoints, which can be connected to multiple networks.
- **Network**: A network is a virtual or logical group of interconnected containers. Each network is isolated from other networks, and allows containers within the same network to communicate with each other.