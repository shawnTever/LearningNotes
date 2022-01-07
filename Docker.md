# 容器技术优势

* 开发和运维人员可以一次创建和配置环境，可以在任何地方运行。

* 开发者可以使用一个标准的镜像来构建一套开发容器

* 运维人员可以直接使用这个容器来部署代码

* docker可以快速创建容器、快速迭代应用程序、全程是可见的

* 让团队中其他人员能够更容易理解应用程序是如何被创建和工作

* docker容器启动轻快

* 内核级别虚拟化，可以实现更高性能和效率

* 更轻松迁移和扩展，几乎可以在当前流行的平台上运行（物理机，虚拟机，公有云，私有云，个人电脑）

* 用户可以擦一个程序从一个平台迁移到另一个平台

* 所有修改都会以增量的方式被分发和更新

# Docker架构

docker是CS（Client、server）架构

**docker daemon**：守护进程，运行在宿主机上，用户通过Docker client客户端Docker命令与Docker daemon交互。

**docker Client**：docker命令行工具是docker的主要方式

**docker image**：镜像，简单说相当于root文件系统

**docker container**：容器就是镜像的一个实例：容器创建，启动，停止，删除，暂停

**docker repository**：仓库是一个代码控制中心，保存镜像

**docker扩展架构**：容器与系统CoreOS，其他定制化操作系统

# 列出镜像 docker images

docker image ls -a

**docker images**

-a :列出本地所有的镜像（含中间映像层，默认情况下，过滤掉中间映像层）；

--digests :显示镜像的摘要信息；

-f :显示满足条件的镜像；

--format :指定返回值的模板文件；

--no-trunc :显示完整的镜像信息；

-q :只显示镜像ID。

# 下载镜像 docker pull

docker pull 镜像名字 <:tags> 从远程仓库抽取镜像

# 删除镜像 docker rmi

docker rmi 镜像名字

docker rmi -f 镜像id ：删除单个镜像

docker rmi -f 镜像名A:tag 镜像名B:tag ：删除多个

docker rmi -f $(docker images -aq)：删除全部

# 删除容器 docker rm

docker rm <-f> 容器id

创建并启动容器 docker run

-i： STDIN 标准输入缓冲器（流）

-t：终端或者模拟终端

-d：以守护进程的方式创建容器

--name：自定义容器名称

eg: 

docker run -i -t  ubuntu:18.04 /bin/bash

docker run -itd  ubuntu

# 在运行的容器中执行命令 docker exec

exit退出容器，容器不会停止

# 在运行的容器中执行命令 docker attach

exit退出容器，容器停止

# 启动容器 docker start

docker start [ID]

# 停止容器 docker stop

docker stop [ID]

# 标记本地镜像 docker tag

标记本地镜像，将其归入某一仓库

docker tag [OPTIONS] IMAGE[:TAG] [REGISTRYHOST/][USERNAME/]NAME[:TAG]

eg:

将镜像ubuntu:15.10标记为 runoob/ubuntu:v3 镜像

docker tag ubuntu:15.10 runoob/ubuntu:v3

REPOSITORY TAG IMAGE ID CREATED  SIZErunoob/ubuntu v3 4e3b13c8a266 3 months ago 136.3 MB

# docker-compose up -d 启动所有服务

# docker-compose ps 检查服务状态

# docker-compose down 停止所有容器服务

# docker-compose stop 停止所有容器服务

# docker ps -a 查看已经在运行的容器

# Docker exec 在运行的容器中执行命令

-d :分离模式: 在后台运行

-i :即使没有附加也保持STDIN 打开

-t :分配一个伪终端