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

<summary>Create configmap and volume. The volume should read data from confimap in a specified path  ?</summary>
<p>

```
kubectl create cm <configmap-name> --from-literal=key=value

Make volume read the values from configmap

apiVersion: v1
kind: pod
metadata:
  Labels:
    app: nginx-pod
spec:
  volumes:
  - name: config-volume
    configMap:
       name: cfgVolume
  containers:
  - name: nginx-pod
    image: nginx:latest
    volumeMounts:
    - name: config-volume
      mountPath: /etc/cfg

 Create a pod with the above created yaml
 kubectl create -f nginx-pod.yaml
 
```
</p>

## kubernetes security context
kubernetes security context defines the priviledge and access control settings for a pod or a container. It allows to set a specific level of permission for a pod or a container. The permissions are limited to certain level. Some of the permission that can be changed are,

1. Changing the user ID or the group ID
2. Linux capabilities ( Giving priviledges to the process )

<summary>Create a pod and add a security context at a pod level for user and group with a sleep of 1200 seconds ?</summary>
<p>

```
kubectl run nginx --image=nginx --restart=Never -- /bin/sh -c "sleep 1200;" -o yaml > nginx-pod.yaml
Open the saved yaml file and check whether we have contents
cat nginx-pod.yaml

Changes to be made on yaml to add the security context

apiVersion: v1
kind: Pod
metadata:
  Labels:
    app: nginx-pod
spec:
  securityContext:
    runAsUser: 100
    runAsGroup: 200
  containers:
  - name: nginx-pod
    image: nginx

Delete the already created pod and recreate the pod again

kubectl create -f nginx-pod.yaml

```
</p>

## kubernetes secrets
A secret is an object which contains a small amount of sensitive data such as password, token or a key. secrets are similar to configmap which holds confidential data. Kubernetes secrets are by default unencrypted in the API's server underlying data store ( etcd ). Anyone who is having access to the API server can able to access the secrets which includes read and write permission.
Whatever the secret we create it will be of type "opque" which is default secret type.

<summary>Create a kubernetes secret which includes username and password ?</summary>
<p>

```
kubectl create secret generic my-secret --from-literal=USERNAME=guest --from-literal=PASSWORD=guest
kubectl get secret

You can view the secrets through below command
kubectl describe secret my-secret

View the secrets created in various namespaces
kubectl get secret --all-namespaces
```
</p>

<summary>Create a kubernetes pod which reads data as a environment variable ?</summary>
<p>

```
kubectl run nginx-pod --image=nginx --restart=Never -o yaml > nginx-secret.yaml
kubectl get pod

Edit the nginx-secret.yaml
spec:
- containers:
   image: nginx
   container: nginx:latest
   env:
   - name: USERNAME
     valueFrom:
       secretKeyFrom:
          name: username
          key: user

Recreate the pod once to reflect the changes
```
</p>

<summary>Create a kubernetes pod which loads the secret as environment variable ?</summary>
<p>

```
kubectl run nginx-pod --image=nginx --restart=Never -o yaml > nginx-secret.yaml
kubectl get pod

Edit the nginx-secret.yaml
spec:
- containers:
    name: nginx
    image: nginx:latest
    envFrom:
       secretFrom:

Recreate the pod once to reflect the changes
```
</p>

<summary>How to create a kubernetes service account with the name guest ?</summary>
<p>

```
kubernetes create sa guest
```
</p>

<summary>How to list all the available kubernetes service account ?</summary>
<p>

```
kubernetes get sa --all-namespaces
```
</p>
