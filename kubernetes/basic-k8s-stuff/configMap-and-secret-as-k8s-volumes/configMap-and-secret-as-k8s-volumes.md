```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mosquitto-config-file
data:
  mosquitto.conf: |
    log_dest stdout
    log_type all
    log_timestamp true
    listener 9001
```
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mosquitto-secret-file
type: Opaque
data:
  secret.file: |
    c29tZXN1cGVyc2VjcmV0IGZpbGUgY29udGVudHMgbm9ib2R5IHNob3VsZCBzZWU=
```
- We can add these files `mosquitto.conf` and `secret.file` from these resources to our pod's container's particular directory.
- For that we need `volumes` and `volumeMounts`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mosquitto
  labels:
    app: mosquitto
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mosquitto
  template:
    metadata:
      labels:
        app: mosquitto
    spec:
      containers:
        - name: mosquitto
          image: eclipse-mosquitto:1.6.2
          ports:
            - containerPort: 1883
          volumeMounts:
            - name: mosquitto-conf
              mountPath: /mosquitto/config
            - name: mosquitto-secret
              mountPath: /mosquitto/secret  
              readOnly: true
      volumes:
        - name: mosquitto-conf
          configMap:
            name: mosquitto-config-file
        - name: mosquitto-secret
          secret:
            secretName: mosquitto-secret-file 
```
- Steps:
- **Adding volume to the pod**:
  1. Add the `Secret` and `ConfigMap` as `volumes` in the pod. For that, under the `spec` of `podTemplate`, in the `volumes` section add the reference of these two resources.
  2. Here `name` is the Name of the volume. `name` under `ConfigMap` is the name of the source `ConfigMap`, which must exist in the cluster beforehand.
  
- **Mounting the volume into the container**:
  1. Now that the `volumes` are added to the pod, we need to mount these volumes into the containers. For that, we need to add reference of `volumes` inside each `container` of the pod, where we want to mount these volumes.
  2. Like in the above deployment YAML, inside the mosquito container, we add these `volumeMounts`. 
  3. In `volumeMounts` there are 3 options:
     - `name`: Name of the `volume` (pod's volume).
     - `mountPath`: Path in the container where these volumes should be mounted.
     - `readOnly`: If it is true, then the application running in the container will not have access to modify these volumes.

In summary, data at first added from `ConfigMap` and `Secret` to pod's volume. From there it can be mounted into each container running inside the pod.