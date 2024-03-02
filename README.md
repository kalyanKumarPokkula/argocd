# Argo CD small example using minikube

Argo CD is a declarative, GitOps continuous delivery tool for Kubernetes. It automatically syncs the desired state of your applications defined in Git repositories to the actual state running in your Kubernetes clusters. Here's a basic guide on how to get started with Argo CD:

## First start the k8s cluster

```
minikube start --driver=docker
```

### Install Argo CD

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Edit the argocd argocd-server

```
kubectl edit svc argocd-server -n argocd
```

change the type clusterIP to NodePort

### you can access the Argo CD UI through port forwarding or by exposing a NodePort/LoadBalancer service

```
minikube service argocd-server -n argocd

```

or

```
kubectl port-forward svc/argocd-server -n argocd 8080:443

```

### getting the argocd-initial-admin-secret password for the secret service

```
kubectl get secret -n argocd
```

```
kubectl edit secret argocd-initial-admin-secret -n argocd
```

### copy the argocd-initial-admin-secret password to the secret service and by default it is encrypted decrypt

```
echo password | base64 --decode
```
