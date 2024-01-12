```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mongodb-configmap
data:
  db_host: mongodb-service
```
- In this ConfigMap, we have a `key-value` pair which we want to set as a `environment_variable` in our pod.
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mongodb-secret
type: Opaque
data:
  username: dXNlcm5hbWU=
  password: cGFzc3dvcmQ=
```
- In this Secret, we have two `key-value` pair which we want to set as a `environment_variable` in our pod.


- So for using these values as environment varibales in the pod configuration of a deployment we do something like this:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongo-express
  labels:
    app: mongo-express
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongo-express
  template:
    metadata:
      labels:
        app: mongo-express
    spec:
      containers:
      - name: mongo-express
        image: mongo-express
        ports:
        - containerPort: 8081
        env:
        - name: ME_CONFIG_MONGODB_ADMINUSERNAME
          valueFrom:
            secretKeyRef:
              name: mongodb-secret
              key: username
        - name: ME_CONFIG_MONGODB_ADMINPASSWORD
          valueFrom:
            secretKeyRef:
              name: mongodb-secret
              key: password
        - name: ME_CONFIG_MONGODB_SERVER 
          valueFrom: 
            configMapKeyRef:
              name: mongodb-configmap
              key: db_host
```
- These values are used for specific containers.
- So these are added in the `env` section under `spec` of `podTemplate`
- `name` is the Name of the environment variable.
- `valueFrom` gives the identity of the configMap or Secret and which pair inside that resource to use.
- So `name` inside the `valueFrom` is the Name of the ConfigMap or Secret and the `key` is used for identifying the `key-pair` value inside data.