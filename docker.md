```bash
docker pull $image_name
# 拉取镜像

docker images
# 查看本地镜像

docker rmi $image_id
# 删除镜像

docker run <options> $image_name
# 运行容器

docker ps
# 查看运行中的容器

docker ps -a
# 查看所有容器

docker stop $container_id
# 停止容器

docker start $container_id
# 启动已停止的容器

docker rm $container_id
# 删除容器
```
