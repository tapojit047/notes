/kind bug

**What steps did you take and what happened:**
- Create a local kind cluster.
- Set `EXP_MACHINE_POOL=true` and `EXP_AKS=true`.
- `clusterctl init` with `--infrastructure azure`.
- `clusterctl generate cluster` with `--flavor aks`.
- Init the target cluster (same as 3).
- `clusterctl move` from local `kind` to target AKS.
- Notice the error below:
```azure
clusterctl move --to-kubeconfig=$AZURE_KUBECONFIG
Performing move...
Discovering Cluster API objects
Moving Cluster API objects Clusters=1
Moving Cluster API objects ClusterClasses=0
Creating objects in the target cluster
Error: action failed after 10 attempts: error creating "infrastructure.cluster.x-k8s.io/v1beta1, Kind=AzureManagedControlPlane" default/new-cluster5: admission webhook "validation.azuremanagedcontrolplanes.infrastructure.cluster.x-k8s.io" denied the request: Spec.ControlPlaneEndpoint.Host: Forbidden: can not be set by the user, will be set automatically by AKS after the cluster is Ready
```

**What did you expect to happen:**

I expect `AzureManagedControlPlane.Spec.ControlPlaneEndpoint.Host` and  `AzureManagedControlPlane.Spec.ControlPlaneEndpoint.Port` can be assigned while performing `clusterctl move`. 

**Anything else you would like to add:**
- The error is raised [here](https://github.com/kubernetes-sigs/cluster-api-provider-azure/blob/main/api/v1beta1/azuremanagedcontrolplane_webhook.go#L101).
- I expect that `clusterctl move` operation to be executed successfully.
- For that, maybe the webhook can check whether the `cluster` object of the `AzureManagedControlPlane` has the `spec.paused` set to `true` and `skip` the two aforementioned conditions of `AzureManagedControlPlane.Spec.ControlPlaneEndpoint.Host` and `AzureManagedControlPlane.Spec.ControlPlaneEndpoint.Port`.
- Or maybe `clusterctl move` should annotate the objects it is `moving` and then webhooks would honour that.

**Environment:**

- cluster-api-provider-azure version: `v1.8.0`
- Kubernetes version: (use `kubectl version`): `v1.26.2`
<!-- - OS (e.g. from `/etc/os-release`): -->

