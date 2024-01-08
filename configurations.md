# Kubernetes Configurations
Kubernetes ConfigMaps and Secrets
## Kubernetes ConfigMaps
<summary>How to create a configmap using kubectl ?</summary>
<p>

```
kubectl create configmap <configmap-name>
or
kubectl create cm <configmap-name>
```
</p>

<summary>How to list all configmaps ?</summary>
<p>

```
kubectl get configmap or kubectl get cm

```
</p>

<summary>How to view the created configmaps ?</summary>
<p>

```
kubectl describe cm <configmap-name>

```
</p>

<summary>Create configmap with any of the literal value ?</summary>
<p>

```
kubectl create cm <configmap-name> --from-literal=key=value

```
</p>

<summary>Create configmap referencing a key value pair from file ?</summary>
<p>

```
kubectl create cm <configmap-name> --from-file=config.txt

```
</p>

<summary>Create a pod and load the environmental values from the configmap that you are creating ?</summary>
<p>

```
kubectl create cm <configmap-name> --from-file=config.txt

kubectl run nginx-pod --image=nginx --restart=Never -o yaml > pod.yaml

open pod.yaml
Make change in the spec.containers field

Example:
envFrom:
- configMapRef:
   name: <configmap-name>

Create the pod again,

kubectl create -f pod.yaml
kubectl describe cm <configmap-name>

```
</p>