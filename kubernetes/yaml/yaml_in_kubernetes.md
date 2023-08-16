# YAML in Kubernetes

## base spec

* Root Level 속성

```yaml
apiVersion:
kind:
metadata:

spec:
```

### apiVersion

* Kind 별 올바른 apiVersion을 작성해야함

| Kind | Version | 
| --- | --- | 
| Pod | v1 | 
| SErvice | v1 | 
| ReplicaSet | apps/v1 | 
| Deployment | apps/v1 | 
  
### kind

### metadata

* 들여쓰기 주의!

```yaml
metadata:
  name: {name}
  labels:
    app: {app}
    name: {label_name}
    type: {type_name}
    ... labels 는 key:value 로 원하는 정보를 설정할 수 있다
```


### spec

* 사양 정보를 작성한다

```yaml
spec:
  containers: # 배열
  - name: {name_1}
    image: {image_name_1} # Docker 가 아닌 다른 이미지 제공자의 경우 이미지를 pull 할 수 있는 전체 경로를 작성한다
  - name: {name_1}
    image: {image_name_1}
```
