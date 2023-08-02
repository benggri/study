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

## JOB
```bash
kubectl create job {pod_name} --image
kubectl create job {pod_name} --image={image_name} --dry-run=client -o yaml > {file_name}.yaml
```

```yml
apiVersion: batch/v1
kind: Job
metadata:
  name: {job_name}
spec:
  completions: {number}
  parallelism: {number}
  backoffLimit: {number} # This is so the job does not quit before it succeeds.
  template:
    spec:
      containers:
      - name: {container_name}
        image: {image_name}
      restartPolicy: Never
```

```yml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: {job_name}
spec:
  schedule: {String:cron_exp}
  jobTemplate:
    spec:
      completions: {number}
      parallelism: {number}
      backoffLimit: {number}
      template:
        spec:
          containers:
          - name: {container_name}
            image: {image_name}
          restartPolicy: Never
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

kubectl edit deployment {deployment_name}
```

```yml
# strategy setting
spec:
  strategy:
    type: Recreate
    type: RollingUpdate
```

## Service
```bash
kubectl get services

kubectl describe service {service_name}
```

## Networkpolicy
```bash
kubectl get networkpolicy
```

```yaml
# https://kubernetes.io/docs/concepts/services-networking/network-policies/
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: test-network-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
    - Ingress # 들어올 수 있는 Source
    - Egress # 나갈 수 있는 Destination
  ingress:
    - from:
        - ipBlock: # 들어올 수 있는 IP 블록 제한
            cidr: 172.17.0.0/16
            except:
              - 172.17.1.0/24
        - namespaceSelector: # label 기반으로 들어올 수 있는 Namespace 제한
            matchLabels:
              project: myproject
        - podSelector: # label 기반으로 들어올 수 있는 Pod 제한
            matchLabels:
              role: frontend
      ports:
        - protocol: TCP
          port: 6379
  egress:
    - to:
        - ipBlock:
            cidr: 10.0.0.0/24
      ports:
        - protocol: TCP
          port: 5978

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
