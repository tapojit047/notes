```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```
- An YAML have 3 basic parts other than `apiVersion` and `Kind`:
  - `metadata`: Metadata of the deployment like name, labels etc. The `labels` is used by other k8s resources like `Service` to find out the deployment.
  - `spec`: specification of the deployment. And `selector` is used to select the pods that are under this deployment. 
  - `status`: it is added automatically by k8s. To keep track of the state of the deployment.
- `template`:
  - `template` under the `spec` of the  deployment is actually `podTemplate`. It is the definition of the pod. So, inside `template`, we have the definition of another k8s resource, in this case, `pod`. So in the same way, like any other k8s resource, it will have `metadata` and `spec`.
  - `metadata` in the `podTemplate` is actually contains `labels` which is used by the deployment to find out these children pods.
  - `spec` contains the specification of the pod. In this case, we have `containers` inside pod. Which actually tells the pod which container to run. 


Resource:
- https://www.youtube.com/watch?v=qmDzcu5uY1I