### DNS records:
- DNS (Domain Name System) records are data files that map domain names to IP addresses. When a user types a domain name in their web browser, the browser sends a DNS query to a DNS server to find the corresponding IP address associated with that domain name. The DNS server responds with the IP address, allowing the browser to connect to the web server that hosts the website.

### Managed DNS Service:
- A managed DNS service is a type of DNS hosting service that provides automated management and maintenance of DNS records for domain names. Instead of managing DNS records manually, users can delegate the management of their DNS records to a DNS hosting provider, which takes care of the technical aspects of DNS management.
- A managed DNS service typically offers features such as:
  - **DNS zone management**: The ability to manage DNS records for one or more domains, including A, AAAA, CNAME, MX, TXT, and NS records.
  - **DNS resolution**: The ability to resolve DNS queries for domain names hosted on the DNS service.
  - **DNS caching**: The ability to cache DNS responses to reduce the response time for subsequent queries.
  - **Load balancing**: The ability to distribute traffic across multiple servers based on DNS responses.
  - **DNSSEC**: The ability to add a layer of security to DNS records by digitally signing them.
  - **API integration**: The ability to integrate with other services through an API.
- Managed DNS services are often used by businesses and organizations that require high availability and reliability for their online services. By delegating DNS management to a managed DNS service, users can focus on other aspects of their business without having to worry about DNS management. Some examples of managed DNS service providers include Amazon Route 53, Google Cloud DNS, Cloudflare DNS, and Microsoft Azure DNS.
### ExternalDNS:
- ExternalDNS is a tool that automates the management of DNS records for Kubernetes resources deployed outside of a cloud provider's managed DNS service. It allows users to define DNS records for Kubernetes resources such as Services, Ingresses, and ExternalIPs using annotations in the Kubernetes manifests.
- ExternalDNS monitors these resources and updates the DNS records dynamically when changes occur. It can work with a variety of DNS providers, including Amazon Route 53, Google Cloud DNS, Azure DNS, and others.
- With ExternalDNS, users can manage DNS records for their Kubernetes resources in a more automated and scalable way, reducing the risk of errors and improving the reliability of their applications. It can also help with managing complex networking scenarios, such as multi-region or multi-cloud deployments, by providing a unified view of DNS records across multiple providers.

### DNS Zone:
- A DNS zone is a portion of the global Domain Name System (DNS) namespace that is managed by a specific organization or entity. A DNS zone is a container that holds information about the domain names and DNS records within that zone.

### Service Principal:
- A service principal is a security identity that is used by applications, services, and tools to access Azure resources. It provides a way for applications to authenticate with Azure Active Directory (Azure AD) and access resources that are secured by Azure AD, without requiring the user to log in.

## Kubelet Identity:
- In Kubernetes, the kubelet is the primary node agent that runs on each worker node in the cluster and is responsible for managing the containers running on that node. The kubelet needs to interact with various Kubernetes API objects to perform its tasks, such as pods, services, and configmaps.
- To authenticate with the Kubernetes API server, the kubelet can use a Kubernetes service account, which is a special type of account that is automatically created by the API server when a new namespace is created. However, managing and securing service account tokens can be complex and error-prone, so Azure Kubernetes Service (AKS) provides the option of using a managed identity to authenticate with the Kubernetes API server.
- A managed identity is a feature of Azure Active Directory that allows you to assign an identity to a resource such as a virtual machine or a container instance. When you enable managed identity for an AKS cluster, it creates a managed identity for each node in the cluster's node pool. This identity is called the kubelet identity, and it is used to authenticate with the Kubernetes API server.
- The kubelet identity allows the kubelet process running on each worker node to authenticate with the Kubernetes API server using Azure Active Directory, without requiring explicit credentials or token management. This simplifies the authentication process and improves the security posture of the cluster.

###  Permissions to modify DNS zone:
