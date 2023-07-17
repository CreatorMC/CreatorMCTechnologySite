# Docker
[菜鸟教程](https://www.runoob.com/docker/docker-tutorial.html)

> 容器是镜像的实例
# 常用命令

## 镜像操作
+ docker images 列出本地主机上的镜像
+ docker pull ubuntu:13.10 获取一个新的镜像
+ docker search rabbitmq 搜索镜像
+ docker pull rabbitmq 拉取（下载）镜像
+ docker rmi hello-world 删除镜像

## 容器操作
+ docker run -it ubuntu /bin/bash 以交互方式从镜像启动一个容器（从容器内退出后会停止运行容器）
+ docker run -id ubuntu /bin/bash 以后台运行方式启动一个容器（从容器内退出后不会停止运行容器）
+ exit 从容器终端中退出
+ docker ps -a 查看所有容器
+ docker ps 只查看运行中的容器
+ docker start b750bbbcfd88 启动一个已停止的容器
+ docker stop b750bbbcfd88 停止一个容器
+ docker restart b750bbbcfd88 重启一个容器
+ docker exec -it 243c32535da7 /bin/bash 进入一个容器
+ docker rm 1e560fca3906 删除一个容器

# Docker部署RabbitMQ
```shell
# RabbitMQ 3.12
docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3.12-management
```

查看镜像
```shell
docker images
```

创建启动容器
```shell
docker run -d --hostname my-rabbit --name rabbitmq --restart always -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin -v /etc/localtime:/etc/localtime:ro -v /usr/local/rabbitmq/data:/var/lib/rabbitmq -p 15672:15672 -p 5672:5672 --privileged=true 1bfc98e879d5
```

查看容器
```shell
docker ps -a
```

进入容器
```shell
docker exec -it rabbitmq /bin/bash
```

开启Web管理页面
```shell
rabbitmq-plugins enable rabbitmq_management
```

> 15672：控制台端口号 Web插件访问端口<br>
5672：应用访问端口号 程序访问端口<br>
控制台端口用于管理rabbitmq，应用访问端口号为应用程序访问<br>

> **如果是在服务器上，需要在防火墙设置中放行以上端口，外部才能访问到！**