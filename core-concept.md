# Kubernetes - Core Concepts

## Kubernetes Namespace

Kuberentes namespace helps different projects, teams or a customer to share a kubernetes cluster. This helps to satify the needs of multiple users or a group of users

<summary>How to create a namespace using kubernetes template yaml ?</summary>
<p>

```
apiVersion: v1
kind: Namespace
metadata:
 name: my-namespace
```
</p>

<summary>How to create a kubernetes namespace through kubectl ?</summary>
<p>

```
kubectl create namespace <namespace-name>
```
</p>

<summary>How to delete the kubernetes namespace through kubectl ?</summary>
<p>

```
kubectl delete namespace <namespace-name>
```
</p>

<summary>How to list all the namespace present in the cluster ?</summary>
<p>

```
kubectl get namespace --all-namespaces
kubectl get namespace -A
```
</p>

<summary>How to describe the namespace ?</summary>
<p>

```
kubectl describe namespace <namespace-name>
```
</p>

<summary>How to get the pods running in the specified namespace ?</summary>
<p>

```
kubectl get pods -n <namespace-name>
```
</p>

<summary>How to get all the labels of the pods running in the specified namespace ?</summary>
<p>
  
```
kubectl get namespace --show-labels
```

</p>

## Kubernetes Pods

<summary>How to create a pod using kubectl ?</summary>
<p>
  
```
kubectl run nginx --image=nginx 
```

</p>

<summary>How to create a pod in a specified namespace using kubectl ?</summary>
<p>
  
```
kubectl run nginx --image=nginx -n default
```

</p>

<summary>How to describe a pod ?</summary>
<p>
  
```
kubectl describe pod <pod-name>
```

</p>

<summary>How to set the resources limits for the pods using kubectl ?</summary>
<p>
  
```
kubectl set resources pod/nginx --image=nginx --limits=cpu=10%,memory=500Mi <pod-name>
```

</p>

<summary>How to delete the pod ?</summary>
<p>
  
```
kubectl delete pod <pod-name>
```

</p>

<summary>How to create the pod using kubernetes tempalte yaml ?</summary>
<p>
  
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-deployment
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
```

</p>

<summary>How to pipe the pod details to the yaml ?</summary>
<p>
  
```
kubectl run nginx --image=nginx -o yaml > pod-details.yaml <pod-name>
```

</p>

<summary>How to get the additional pod details using kubectl ?</summary>
<p>
  
```
kubectl get pod <pod-name> -o wide
```

</p>

