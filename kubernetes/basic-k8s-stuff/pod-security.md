# PodSecurity:
The Pod Security Standard (PSS) in Kubernetes is a set of guidelines and recommendations for securing pods within a Kubernetes cluster. The Pod Security Standard is not a standalone tool or technology but rather a set of best practices and configurations that can be applied to Kubernetes clusters to enhance security. It helps organizations define and enforce security policies related to pod creation and deployment.
Key aspects covered by the Pod Security Standard include:
- **Privilege Escalation Prevention**: Ensuring that pods do not run with unnecessary privileges or capabilities that could be exploited.

## root user:
In Unix-like operating systems, including Linux, the root user is a superuser or administrator account that has the highest level of privileges. The root user is also known as the superuser because it can execute any command and perform any action on the system. Here are some key characteristics of the root user:
- **Unrestricted Access**: The root user has unrestricted access to all files, directories, and system resources. It can read, write, and execute any file, change permissions, and modify system configuration.
- **System-wide Configuration**: The root user has the authority to modify system-wide configurations, install or remove software, and make changes to critical files that affect the overall functionality of the operating system.
- **Process Control**: The root user can manage processes, including starting or stopping system services and killing processes owned by any user.
- **Device Access**: The root user can access and configure hardware devices, including storage devices, network interfaces, and other peripherals.

While the root user is essential for system administration tasks, granting unrestricted access to the root account also introduces security risks. Here's how it can be harmful:
- **Security Vulnerabilities**: If a malicious actor gains access to the root account, they can exploit vulnerabilities, install malware, or perform unauthorized actions with significant consequences.
- **Accidental Mistakes**: Even well-intentioned actions by administrators can lead to unintended consequences. Executing a wrong command as the root user could potentially damage the system or result in data loss.
- **Unauthorized System Changes**: Without proper controls, multiple users or processes running as root could make simultaneous changes to the system, leading to conflicts, instability, or unpredictable behavior.

To mitigate these risks, best practices in system administration involve limiting the use of the root account and employing the principle of least privilege. In the context of containerized environments like Kubernetes, avoiding running processes as the root user within containers is a security measure to reduce the impact of potential security vulnerabilities. Containers are encouraged to run with non-root users and have restricted capabilities to enhance security.

### Effects of running a container with root user:
Running a container in a pod with the root user can potentially introduce security risks and have harmful effects. Here are some reasons why running containers as the root user may be undesirable:
- Increased Attack Surface: Containers running as the root user have elevated privileges, and if a container is compromised, an attacker with access to the root user can potentially perform more harmful actions. This increases the attack surface and the potential impact of security vulnerabilities.
- Filesystem Manipulation: The root user within a container has unrestricted access to the container's filesystem and can modify or delete any file. If an attacker gains control of a container running as root, they can manipulate files, configuration files, and even install malicious software.
- Privilege Escalation: Running processes as the root user increases the risk of privilege escalation. If an attacker manages to exploit a vulnerability in a containerized application, they may be able to escalate their privileges to root within the container, potentially leading to broader system compromise.
- Host System Impact: Containers share the underlying kernel with the host system. If a container running as root is compromised and an attacker gains kernel-level access, they could potentially impact the entire host system, not just the container.
- Security Best Practices: Running containers as a non-root user follows the principle of least privilege, which is a best practice in security. Limiting privileges to only what is necessary for the application helps minimize the potential damage in case of a security incident.

To mitigate these risks, it is recommended to follow security best practices when configuring containers in Kubernetes:
- Run as Non-Root: Whenever possible, configure containers to run as non-root users. This helps reduce the impact of potential security vulnerabilities by limiting the privileges of the processes running inside the container.
- Use Least Privilege: Only grant the necessary capabilities and permissions to the containerized application. This reduces the attack surface and helps prevent unauthorized access or modifications.
- Security Contexts: Kubernetes allows you to define security contexts at the pod and container level. Security contexts include settings such as the user ID, group ID, capabilities, and more. Utilize these settings to enforce security policies.

- By following these best practices, you can enhance the security of your containerized workloads in Kubernetes and reduce the risk of security incidents.

￼### Running Container inside pod as non root user:
- To run a container inside a pod as a non-root user in Kubernetes, you can set the security context for the pod or container. Here's how you can achieve this:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: yourpod
spec:
  containers:
  - name: yourcontainer
    image: your-image-name
    securityContext:
      runAsUser: 1000  # Replace 1000 with the desired non-root user ID
```

### Security Context: 
In Kubernetes, the `securityContext` field is a part of the Pod and Container specifications. It allows you to define various security-related settings and constraints for pods and containers. This field helps you control the security aspects of your workloads by specifying parameters such as user and group IDs, capabilities, and more. Here's an overview of some common fields within securityContext:
- runAsUser and runAsGroup: These settings specify the UID (User ID) and GID (Group ID) for the main process running inside the container. By setting these values, you can control the user under which the processes inside the container run.
```yaml
securityContext:
  runAsUser: 1000
  runAsGroup: 1000
```
- capabilities: This setting allows you to drop or add specific Linux capabilities for the container. Capabilities are fine-grained privileges that processes can have. Dropping unnecessary capabilities reduces the attack surface.
```yaml
securityContext:
  capabilities:
    drop:
      - "NET_ADMIN"
```
- readOnlyRootFilesystem: When set to true, this makes the container's root filesystem read-only. It enhances security by preventing processes within the container from writing to the root filesystem.
```yaml
securityContext:
  readOnlyRootFilesystem: true
```
- allowPrivilegeEscalation: When set to false, this prevents processes inside the container from gaining additional privileges.
```yaml
securityContext:
  allowPrivilegeEscalation: false
```


- Running as Root: