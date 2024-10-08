# docker常用命令二

## 启动停止容器

```
#启动|停止|重启 指定容器  
docker start|stop|restart [id]   
# 暂停|恢复 某一容器的所有进程  
docker pause|unpause [id]  
# 杀死一个或多个指定容器进程  
docker kill -s KILL [id]  
# 停止全部运行的容器  
docker stop `docker ps -q`  
# 杀掉全部运行的容器  
docker kill -s KILL `docker ps -q`
```

## 交互式进入容器

```
sudo docker exec -it {{containerName or containerID}} bash  
sudo docker exec -i {{containerName or containerID}} bash  
sudo docker exec -t {{containerName or containerID}} bash  
sudo docker exec -d {{containerName or containerID}} bash  

只用 -i 参数，由于没有分配伪终端，看起来像pipe执行一样。但是执行结果、命令返回值都可以正确获取  
只用 -t 参数，则可以看到一个 console 窗口，但是执行命令会发现由于没有获得stdin的输出，无法看到命令执行情况  
使用 -it 时，则和我们平常操作 console 界面类似，而且也不会像attach方式因为退出，导致整个容器退出  
使用 -d 参数，在后台执行一个进程。如果一个命令需要长时间进程，会很快返回  
```

## Docker attach

```
# Docker attach可以attach到一个已经运行的容器的stdin，然后进行命令执行的动作  
docker attach {{containerName or containerID}}
```

## 查看容器的root用户密码

```
# 因为Docker容器启动时的root用户的密码是随机分配的。所以，通过这种方式就可以得到容器的root用户的密码  
docker logs <容器名orID> 2>&1 | grep '^User: ' | tail -n1
```

## 容器于宿主拷贝文件

```
docker cp [OPTIONS] CONTAINER:SRC_PATH  DEST_PATH
docker cp [OPTIONS] SRC_PATH  CONTAINER:DEST_PATH
# 本地文件上传到对应容器的目录
docker cp local.sh [CONTAINERid]:[TagPath]
```

## 一个容器连接到另一个容器

```
docker run -i -t --name sonar -d -link mmysql:db  tpires/sonar-server sonar
```

## 导入导出容器

```
# 支持远程文件 .tar, .tar.gz, .tgz, .bzip, .tar.xz, .txz
docker import
# 导出
docker export [id] >~/Downloads/ubuntu_nexus.tar
```

## 镜像常用命令

```
# 列出本地所有镜像
docker images
# 本地镜像名为 ubuntu 的所有镜像
docker images ubuntu
# 查看指定镜像的创建历史
docker history [id]
# 本地移除一个或多个指定的镜像
docker rmi
# 移除本地全部镜像
docker rmi `docker images -a -q`
# 指定镜像保存成 tar 归档文件， docker load 的逆操作
docker save
# 将镜像 ubuntu:14.04 保存为 ubuntu14.04.tar 文件
docker save -o ubuntu14.04.tar ubuntu:14.04
# 从 tar 镜像归档中载入镜像， docker save 的逆操作
docker load
# 上面命令的意思是将 ubuntu14.04.tar 文件载入镜像中
docker load -i ubuntu14.04.tar
docker load < /home/save.tar
# 构建自己的镜像
docker build -t <镜像名> <Dockerfile路径>
docker build -t xx/gitlab .
```
