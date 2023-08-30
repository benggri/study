# Security In Docker

Docker 에서 이미지를 실행하면 root 사용자로 실행된다

```bash
docker run {image} sleep 1000
```

특정 사용자로 실행하기 위해서는 아래의 명령어를 이용한다

```bash
docker run --user={user_name} {image} sleep 1000
```

- 컨테이너 안의 roo 와 시스템의 root 는 다르다
- 그래서 권한을 설정해주어야한다

Linux 에서 root 사용자가 할 수 있는 행위의 목록은 아래서 확인한다

```
/usr/include/linux/capability.h
```

## 권한 설정
docker run 을 하여 권한을 추가하거나 제거할 수 있다

### 권한 추가

```bash
docker run --cap-add {권한명} {image}
# docker run --cap-add MAC_ADMIN {image}
```

### 권한 제거

```bash
docker run --cap-drop {권한명} {image}
## docker run --cap-drop KILL {image}
```

### 모든 권한을 다 주는 것

```bash
docker run --privileged {image}
```
