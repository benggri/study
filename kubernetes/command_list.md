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

## ReplicaSets
```bash
kubectl edit replicasets {replicasets_name}

# Replica 갯수 수정
kubectl scale replicasets {replicasets_name} --replicas={number}
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

kubectl run {pod_name} --image={image_name} -l {key}={value}
# nginx 이미지를 사용해 nginx 라는 이름과 labels tier=db pod 생성 및 실행
kubectl run nginx --image=nginx -l tier=db

kubectl run {pod_name} --image={image_name} -l {key}={value} --port={port_number}
# 이미지 nginx , POD 이름 nginx , labels tier=db, PORT 8080 pod 생성 및 실행
kubectl run nginx --image=nginx -l tier=db --port=8080

kubectl run {pod_name} --image={image_name} -l {key}={value} --port={port_number} --expose
# 이미지 nginx , POD 이름 nginx , labels tier=db, PORT 8080 pod 생성 및 실행
# service 까지 생성
kubectl run nginx --image=nginx -l tier=db --port=8080 --expose


kubectl get pods --selector {key}={value}
```

### POD Volume Mounts
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp
spec:
  containers:
  - name: event-simulator
    image: kodekloud/event-simulator
    env:
    - name: LOG_HANDLERS
      value: file
    volumeMounts:
    - mountPath: /log
      name: log-volume

  volumes:
  - name: log-volume
    hostPath:
      # directory location on host
      path: /var/log/webapp
      # this field is optional
      type: Directory
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

kubectl get deployment --namespace={namespace_name}

kubectl create deployment {deployment_name} --image={image_name} --replicas={replicas_number}
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

# 서비스 생성
kubectl expose pod {pod_name} --port={port_number} --name {service_name}
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

### ingress
```bash
kubectl get ingress --all-namespaces
kubectl describe ingress --namespace {namespace_name}
kubectl edit ingress --namespace {namespace_name}
```

## ConfigMap
```bash
kubectl create configmap {configmap_name} --namespace {namespae_name}
```

## Role
```bash
kubectl get roles
```

## RoleBindings
```bash
kubectl get rolebindings
```

## ClusterRoles
```bash
kubectl get clusterroles
```

## ClusterRoleBindings 
```bash
kubectl get clusterrolebindings 
```





## Namespace
```bash
kubectl create namespace {namespace_name}
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
kubectl create serviceaccount {service_account_name} --namespace {namespace_name}
```


## Persistent Volume

### Persistent Volume
```bash
kubectl get pv
```

```yaml
# https://kubernetes.io/ko/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#%ED%8D%BC%EC%8B%9C%EC%8A%A4%ED%84%B4%ED%8A%B8%EB%B3%BC%EB%A5%A8-%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0
apiVersion: v1
kind: PersistentVolume
metadata:
  name: task-pv-volume
  labels:
    type: local
spec:
  storageClassName: manual
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```

### Persistent Volume Claim
```bash
kubectl get pvc
```

```yaml
# https://kubernetes.io/ko/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#%ED%8D%BC%EC%8B%9C%EC%8A%A4%ED%84%B4%ED%8A%B8%EB%B3%BC%EB%A5%A8-%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: task-pv-claim
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```

### POD

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp
spec:
  containers:
  - name: event-simulator
    image: kodekloud/event-simulator
    env:
    - name: LOG_HANDLERS
      value: file
    volumeMounts:
    - mountPath: /log
      name: log-volume
  volumes:
  - name: log-volume
    persistentVolumeClaim:
      claimName: claim-log-1
```
