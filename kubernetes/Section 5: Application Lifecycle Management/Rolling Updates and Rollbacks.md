# Rolling Updates and Rollbacks

## rollout

```bash
# 상태 확인
kubectl rollout status deployment/{deployment_name}

# 이력 확인
kubectl rollout history deployment/{deployment_name}
```

## 배포 전략
- Recreate
  - 다 내리고 새로 올림
  - 다 내리고 새로 올리는 동안 Application 이 중지됨
- Rolling Update
  - 하나씩 내렸다 새로 올

```bash
# 파일 내용 수정 후 apply
kubectl apply -f {file_name}.yaml

# set 명령을 이용해 image 버전 변경
kubectl set image deployment/{deployment_name} \ {container_name}={image_name}:{version}
# => 이렇게 하면 yaml 파일에서 관리하고 있지 않기 때문에 권장하지 않음
```

## Rollback

```bash
kubectl rollout undo deployment/{deployment_name}
```

---

## Summarize Commands

### create

```bash
kubectl create -f {file_name}.yaml
```

### get

```bash
kubectl get deployments
```

### update

```bash
kubectl apply -f {file_name}.yaml

kubectl set image deployment/{deployment_name} {container_name}={image_name}:{version}
```

### status

```bash
kubectl rollout status deployment/{deployment_name}

kubectl rollout history deployment/{deployment_name}
```

### Rollback

```bash
kubectl rollout undo deployment/{deployment_name}
```

