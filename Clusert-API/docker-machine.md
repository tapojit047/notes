# Docker Machine
- Docker Machine was a tool provided by Docker that allowed users to create and manage Docker hosts on local machines or remote cloud providers. It was particularly useful for setting up Docker on systems that did not natively support Docker, such as Windows or macOS.
- Here are some key features and functionalities of Docker Machine:
  - **Create Docker Hosts**: Docker Machine allowed users to create virtual machines running Linux (or other supported operating systems) and automatically install Docker on them. These virtual machines acted as Docker hosts and could run Docker containers.
  - **Multiple Drivers:** Docker Machine supported various "drivers," which were plugins that allowed it to create Docker hosts on different platforms. Popular drivers included VirtualBox (for local development), Amazon Web Services (AWS), Microsoft Azure, Google Cloud Platform (GCP), and more.
  - **Interact with Docker CLI:** Once a Docker host was created using Docker Machine, the Docker CLI (command-line interface) on the local machine could be configured to communicate with the Docker daemon running on the remote Docker host. This enabled users to build, run, and manage containers on the remote machine as if they were running locally.
  - **Swarm Setup:** Docker Machine could also be used to create Docker Swarm clusters, which are groups of Docker hosts acting as a single virtual Docker host, allowing users to deploy applications across multiple machines for high availability and scalability.
  - **Managing Multiple Environments:** Docker Machine made it easy to manage multiple Docker environments, such as having separate environments for development, testing, and production, without needing to install Docker directly on the host machine.
- Docker Machine was considered deprecated in favor of using Docker Desktop on macOS and Windows for local development, and using Docker's native capabilities on supported cloud providers for remote setups. Docker has been focusing on improving the Docker Desktop and Docker native experiences on different platforms.

## Difference of Docker Machine and Docker Engine:
- **Docker Engine:** When people say “Docker” they typically mean **Docker Engine**, the client-server application made up of the Docker daemon, a REST API that specifies interfaces for interacting with the daemon, and a command line interface (CLI) client that talks to the daemon (through the REST API wrapper). Docker Engine accepts **docker** commands from the CLI, such as **docker run <image>**, **docker ps** to list running containers, **docker image ls** to list images, and so on.
- **Docker Machine:** Docker Machine is a tool for provisioning and managing your Dockerized hosts (hosts with Docker Engine on them). Typically, you install Docker Machine on your local system. Docker Machine has its own command line client **docker-machine** and the Docker Engine client, **docker**. You can use Machine to install Docker Engine on one or more virtual systems. These virtual systems can be local (as when you use Machine to install and run Docker Engine in VirtualBox on Mac or Windows) or remote (as when you use Machine to provision Dockerized hosts on cloud providers). The Dockerized hosts themselves can be thought of, and are sometimes referred to as, managed “machines”.

## How to install Docker Machine:
```bash
curl -OL https://github.com/rancher/machine/releases/download/v0.15.0-rancher99/rancher-machine-amd64.tar.gz
tar -xzvf rancher-machine-amd64.tar.gz
chmod +x rancher-machine
mv rancher-machine /bin/docker-machine
```

## Using Docker Machine to provision hosts on cloud providers (azure):
- Docker Machine driver plugins are available for many cloud platforms, so you can use Machine to provision cloud hosts. When you use Docker Machine for provisioning, you create cloud hosts with Docker Engine installed on them.
- Install and run Docker Machine, and create an account with the cloud provider.
- Then you provide account verification, security credentials, and configuration options for the providers as flags to `docker-machine create`. The flags are unique for each cloud-specific driver.
- For example for creating vms in azure: 
```azure
  $ docker-machine create --driver azure --azure-subscription-id <subs-id> --azure-tenant-id <tenant-id> --azure-client-id <client-id> --azure-client-secret <client-secret> --azure-resource-group <resource-group-name> --azure-custom-data <path-to-script> <machine-name>
```
- The `docker-machine create` command: The `docker-machine create` command typically requires that you specify, at a minimum:
  - `--driver` - to indicate the provider on which to create the machine
  - Account verification and security credentials (for cloud providers), specific to the cloud service you are using
  - `<machine>` - name of the host you want to create

- For convenience, `docker-machine` uses sensible defaults for choosing settings such as the image that the server is based on, but you override the defaults using the respective flags, such as --digitalocean-image. This is useful if, for example, you want to create a cloud server with a lot of memory and CPUs, rather than the default behavior of creating smaller servers.

### Resources:
- [Docker Machine](https://gcbw.github.io/docker.github.io/machine/)
- [Docker Machine Repo](https://github.com/docker/machine)
- [Rancher Docker Machine Repo](https://github.com/rancher/machine/tree/master)
- [Use Docker Machine to provision hosts on cloud providers](https://gcbw.github.io/docker.github.io/machine/get-started-cloud/)
- [Microsoft Azure](https://gcbw.github.io/docker.github.io/machine/drivers/azure/)