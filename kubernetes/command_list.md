# Kubernetes Command List

## Command 
```bash
kubectl get
kubectl set
kubectl describe
kubectl create 
kubectl apply 
```

## POD
```bash
# pod list
kubectl get pods

kubectl describe pod {pod_name}

kubectl get pod -o yaml
kubectl get pod {pod_name} -o yaml > {file_name}.yaml

kubectl apply -f {file_name}.yaml
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
