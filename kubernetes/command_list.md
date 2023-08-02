# Kubernetes Command List

## Command 
```bash
kubectl get
kubectl get [type] --selector {key}={value}
kubectl get all --selector {key}={value},{key}={value}
kubectl set
kubectl describe
kubectl run {pod_name}
kubectl create [type] {type_name}
kubectl edit [type] {type_name}
kubectl replace
kubectl apply
kubectl taint nodes {node_name} {key}={value}:{schedule}
kubectl label [type] {type_name} {key}={value}
kubectl top [type]

```

## POD
```bash
# pod list
kubectl get pods

kubectl describe pod {pod_name}

kubectl get pod -o yaml
kubectl get pod {pod_name} -o yaml > {file_name}.yaml

kubectl apply -f {file_name}.yaml

kubectl run {pod_name} --image={image_name}
# nginx 이미지를 사용해 nginx 라는 이름으로 pod 생성 및 실행
kubectl run nginx --image=nginx
kubectl get pods --selector {key}={value}
```

## Node
```bash
kubectl get nodes

kubectl describe node {node_name}

kubectl taint nodes {node_name} {key}={value}:{schedule}
kubectl label nodes 경
kubectl replace --force -f {file_name}.yaml
```

## Deployment
```bash
kubectl get deployments

kubectl describe deployment {deployment_name}
```

## Containers
```bash

```

## Service Account
```bash
# service account list
kubectl get serviceaccounts

# detail service account
kubectl describe serviceaccount {namespace}

# create service account
kubectl create serviceaccount {service_account_name}
```
