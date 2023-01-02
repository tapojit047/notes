## Chapter 2:
**netfilter**: 
- https://www.digitalocean.com/community/tutorials/a-deep-dive-into-iptables-and-netfilter-architecture

**IPVS**: 
- IPVS (IP Virtual Server) is a load balancing solution for Linux systems that allows a network administrator to distribute network traffic across multiple servers. It can be used to balance load on web servers, FTP servers, or other types of servers that handle network traffic. IPVS operates at the Layer 4 of the OSI model, which means it can direct traffic based on the IP address and port number of incoming packets. It can be used in conjunction with other Linux tools, such as iptables, to provide a complete load balancing solution.

**eBPF**: 
- In simple terms, eBPF (extended Berkeley Packet Filter) is a feature in the Linux kernel that allows you to attach small programs, called eBPF programs, to various hooks in the kernel. These programs can be used to monitor and modify kernel behavior in a variety of ways, such as filtering network traffic, tracing system calls, and more. They are written in a restricted form of C and are compiled into a bytecode that can be loaded into the kernel at runtime. eBPF is a powerful tool that is used in a variety of applications, including networking, security, and performance monitoring.

**tcpdump**: 
- TCPDump is a command-line packet analyzer tool that allows you to capture and display packets that are transmitted over a network. It can be used to troubleshoot network problems, monitor network traffic, and more.
In simple terms, TCPDump allows you to see the data that is being sent over a network in real-time. It displays the packets in a human-readable format, showing the source and destination addresses, the type of packet, and other relevant information. You can use TCPDump to filter the packets that are displayed based on various criteria, such as the type of packet, the source or destination address, and more. This makes it a useful tool for diagnosing and debugging network issues.

### Network Troubleshooting Tools:
**Ping**: 
- ping is a simple program that sends ICMP ECHO_REQUEST packets to networked
  devices. It is a common, simple way to test network connectivity from one host
  to another.

**traceroute**: 
- traceroute shows the network route taken from one host to another. This
allows users to easily validate and debug the route taken (or where routing fails)
from one machine to another.

**dig**: 
- dig is a DNS lookup tool. You can use it to make DNS queries from the
command line and display the results.

**nmap**:
- nmap is a port scanner, which allows you to explore and examine services on
your network.

**nestat**:
- netstat can display a wide range of information about a machine’s network
stack and connections.

**netcat**:
- netcat is a multipurpose tool for making connections, sending data, or listening
on a socket.
- It can be helpful as a way to “manually” run a server or client to
inspect what happens in greater detail.

**Openssl**:
- OpenSSL is a software library that is used to secure communication over computer networks. It provides a set of cryptographic functions and protocols that can be used to secure communication and protect data from unauthorized access. OpenSSL is commonly used to secure web traffic, protect data in transit, and provide authentication and authorization for users. It is an open-source software, which means that it is freely available for anyone to use and modify.
- The OpenSSL technology powers a substantial chunk of the world’s HTTPS
connections.

**cURL**:
- cURL is a command-line tool and library for transferring data with URLs. It is often used to send and receive data over the internet, such as downloading a file from a web server or uploading data to a server. cURL supports various protocols, including HTTP, HTTPS, FTP, and LDAP. It can be used to make HTTP requests, send emails, and perform other internet-related tasks. cURL is widely used by developers to test and automate web applications, and is available on most operating systems.
- cURL is a data transfer tool that supports multiple protocols, notably HTTP and
HTTPS.
- cURL commands are of the form curl [options] <URL>
- For [more](https://www.freecodecamp.org/news/how-to-start-using-curl-and-why-a-hands-on-introduction-ea1c913caaaa/) 