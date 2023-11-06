# tekton-argo-minikube


You can setup your own machine using the following steps : 

1. Install minikube on your local machine :

Use the Minikube documentation to install minikube .

```
https://minikube.sigs.k8s.io/docs/start/
```

2. Setup your favourite IDE to code the microservices and k8s objects :

```
https://github.com/orgs/Lord-of-the-Pods/repositories
```


3. Create the following namespaces in K8s :

CICD for your tekton pieplines
ArgoCd for your Argocd Gitops
Namespace for your microservices

```
kubectl create namespace cicd            

kubectl create namespace lotp

kubectl create namespace argocd
```

## Setup Tekton on Minikube 

### 1. Install Tekton Pipelines on minikube 

```
kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml

kubectl get pods --namespace tekton-pipelines --watch
```

### 2. Install Tekton Dashboard on minikube
```
kubectl apply --filename https://storage.googleapis.com/tekton-releases/dashboard/latest/release.yaml

kubectl get pods --namespace tekton-pipelines --watch
```

### 3. Access Tekton
```
kubectl -n argocd port-forward svc/argocd-server 9001:443
```

## Setup ArgoCD on Minikube 

### 1. Install Argo CD on minikube 
```
git clone https://github.com/argoproj/argo-cd.git
cd ~/learning/argo/argocd/argo-cd/manifests
kubectl -n argocd apply -f install.yaml
```

### 2. Access Argo
```
kubectl --namespace tekton-pipelines port-forward svc/tekton-dashboard 9097:9097
```
