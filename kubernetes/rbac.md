# Role Based Access Control (RBAC)
- Role-based access control provides a mechanism for restricting both access to and  actions on Kubernetes APIs to ensure that only authorized users have access.
- RBAC is a critical component to both harden access to the Kubernetes cluster where you are deploying your application.
- Every request to Kubernetes is first authenticated.
- Once users have been authenticated, the authorization phase determines whether they are authorized to perform the request. Authorization is a combination of the identity of the user, the resource (effectively the HTTP path), and the verb or action the user is attempting to perform. If the particular user is authorized to perform that action on that resource, then the request is allowed to proceed. Otherwise, an HTTP 403 error is returned. Let’s dive into this process.
- Every request to Kubernetes is associated with some identity. Even a request with no identity is associated with the system:unauthenticated group.

### Role: 
A role is a set of abstract capabilities. For example, the appdev role might represent the ability to create Pods and Services. 
### Role Binding: 
A role binding is an assignment of a role to one or more identities. Thus, binding the appdev role to the user identity alice indicates that Alice has the ability to create Pods and Services.
