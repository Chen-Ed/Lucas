# docker常用命令一

## 查看docker信息

```
# 启动关闭docker  
sudo systemctl restart|start|stop docker  
# 查看docker版本  
docker version  
# 显示docker系统的信息  
docker info  
# 故障检查  
service docker status   
# 查看当前运行的容器  
docker ps  
# 查看全部容器  
docker ps -a  
# 查看全部容器的id和信息  
docker ps -a -q  
# 查看全部容器占用的空间  
docker ps -as  
# 查看一个正在运行容器进程，支持 ps 命令参数  
docker top  
# 查看容器的示例id  
sudo docker inspect -f  '{{.Id}}' [id]  
# 检查镜像或者容器的参数，默认返回 JSON 格式  
docker inspect  
# 返回 ubuntu:14.04  镜像的 docker 版本  
docker inspect --format '{{.DockerVersion}}' ubuntu:14.04  
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ubuntu:14.04  
```

## 查看日志

```
# 日志信息
docker logs -f <容器名orID>
```

## 容器同步命令

```
# 保存对容器的修改  
docker commit  
# 保存某个容器成为一个镜像  
docker commit -a "user" -m "commit info" [CONTAINER] [imageName]:[imageTag]  
# 推送一个容器到中心仓库  
docker login --username=[userName] --password=[pwd] [registryURL]  
## 建议登录后查看 docker info  
docker tag [imageID] [remoteURL]:[imageTag]  
docker push [remoteURL]:[imageTag]  
# 拉取提交的容器  
docker pull [remoteURL]:[imageTag]  
# 对比容器的改动  
docker diff  
# 附加到一个运行的容器上  
docker attach  
```

## 创建删除容器

```
# 创建一个容器命名为 test 使用镜像daocloud.io/library/ubuntu  
docker create -it --name test daocloud.io/library/ubuntu  
# 创建并启动一个容器 名为 test 使用镜像daocloud.io/library/ubuntu  
docker run --name test daocloud.io/library/ubuntu  
# 删除一个容器  
docker rm [容器id]  
# 删除所有容器  
docker rm `docker ps -a -q`  
# 根据Dockerfile 构建  
docker build -t [image_name] [Dockerfile_path]  
```

## docker容器随系统自启

docker run --restart=always

## 容器资源限制参数

```
# 限制内存最大使用  
-m 1024m --memory-swap=1024m  
# 限制容器使用CPU  
--cpuset-cpus="0,1"  
```
