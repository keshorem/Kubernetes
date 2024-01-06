Kubernetes - Core Concepts

Kubernetes Namespace
Kuberentes namespace helps different projects, teams or a customer to share a kubernetes cluster. This helps to satify the needs of multiple users or a group of users

How to create a namespace using kubernetes template yaml ?
  
apiVersion: v1
kind: Namespace
metadata:
 name: my-namespace

