```yaml
# docker.env
변수=값
IMG_VERSION=0.0.1
VERSION=${IMG_VERSION}
IMAGE=IMAGE_NAME
DOCKER_FILE=./Dockerfile
```

docker compose --env-file ./docker_env/docker.env build --no-cache

docker push {image_name}:{version}

docker run -i -t --name {container_name} {image_name}:{version} /bin/bash

docker ps -a

docker rm {container_id}

docker rmi {image_name}:{version}
