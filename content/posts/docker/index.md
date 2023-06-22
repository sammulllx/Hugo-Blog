---
title: "docker"
date: 2023-05-17T17:24:41+08:00
# weight: 1
# aliases: ["/first"]
tags: ["docker"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Desc Text."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---



## 命令

```bash
#把用户加入 Docker 用户组,避免每次 sudo
sudo usermod -aG docker $USER
#查看当前用户所属组
groups

#运行docker
# service 命令的用法
sudo service docker start
# systemctl 命令的用法(更先进)
sudo systemctl start docker

# 列出本机的所有 image 文件。
docker image ls

# 删除 image 文件
docker image rm [imageName]

#将 image 文件从仓库抓到本地,其中library是 image 文件所在的组
docker image pull library/hello-world
#Docker 官方提供的 image 文件，都放在library组里面，所以它的是默认组，可以省略
docker image pull hello-world

#查看本机 image 文件
docker image ls

#运行 image 文件(image 文件没有会自动从仓库抓取)
docker container run hello-world

#在命令行体验 ubuntu 系统,-i(interactive)-t(tty)
docker container run -it ubuntu bash

#对不会自动终止的容器,必须手动终止
docker container kill [containerID]

# 列出本机正在运行的容器(新版 推荐)
docker container ls
#或(旧版ps 代表 process status)
docker ps 

# 列出本机所有容器，包括终止运行的容器
docker container ls --all

#容器文件终止后依然会占用硬盘空间,需要彻底删除
docker container rm [containerID]


#启动已经生成、已经停止运行的容器文件。
docker container start [containerID]

#终止容器运行(比 kill 效果弱)
docker container stop [containerID]


#查看 docker 容器的输出,即容器里面 shell 的标准输出
docker container logs [containerID]


#进入一个正在运行的容器(如果 docker run的时候没有加-it 参数)
docker container exec -it [containerId] /bin/bash


#从正在运行的 docker 容器里面,将文件(文件夹)拷贝到本机当前目录(container 可以省略)
docker container cp [containerId]:/file/path /host/path

```

## 换源

[Docker 资源汇总 | 菜鸟教程](https://www.runoob.com/docker/docker-resources.html)[Docker 资源汇总 | 菜鸟教程](https://www.runoob.com/docker/docker-resources.html)

运行脚本文件 change.sh

```bash
#! /bin/bash

date "+%Y年%m月%d日 周%w %H:%M:%S"
echo '为 Docker 更换官方国内源加速下载'
cat > /etc/docker/daemon.json << EOF
{
 "registry-mirrors": ["https://registry.docker-cn.com"]
}
EOF
service docker restart
docker info|grep "Registry Mirrors" -A 1
echo '显示 registry.docker-cn.com 即换源成功'
```

运行脚本文件 change.sh(换阿里源)

```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://31agitg6.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

[docker 容器中换源](https://blog.csdn.net/u013788943/article/details/109029723)

## 实操

### ubuntu

普通方式

```bash
 docker container run -it ubuntu /bin/bash
```

compose.yaml 文件:

```yaml
services:
  my-ubuntu-container:
    image: ubuntu
    container_name: ubuntu
    tty: true
    stdin_open: true
    volumes:
      - /home/sammul/tmp:/tmp
      - data:/home
volumes:
  data:
#实际生成的 volume 名为[文件夹名]_data 比如ubuntu_data
```

运行:

```bash
#开始运行-d (detach)后台运行
docker-compose up -d
#停止
docker-compose stop 
#开始
docker-compose start 
#删除-v (volume)不加则不会删除 volume 文件夹
docker-compose down -v
#查看 所有运行中的 compose
docker-compose ls
#查看 volume
docker volume ls
```

### portainer

普通命令

```bash
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

安装中文版[github 仓库](https://github.com/outlovecn/portainer-cn)

```bash
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data outlovecn/portainer-cn:latest
```



升级 portainer:

```bash
docker stop portainer
docker rm portainer
docker pull portainer/portainer-ce:latest
docker run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```



compose.yaml:

```yaml
services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - data:/data
    ports:
      - "8000:8000"
      - "9443:9443"
volumes:
  data:
```

### wordpress-mysql

compose.yaml:

```yaml
services:
  db:
    # We use a mariadb image which supports both amd64 & arm64 architecture
    image: mariadb:10.6.4-focal
    # If you really want to use MySQL, uncomment the following line
    #image: mysql:8.0.27
    command: '--default-authentication-plugin=mysql_native_password'
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=somewordpress
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=wordpress
    expose:
      - 3306
      - 33060
  wordpress:
    image: wordpress:latest
    ports:
      - 80:80
    restart: always
    environment:
      - WORDPRESS_DB_HOST=db
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=wordpress
      - WORDPRESS_DB_NAME=wordpress
volumes:
  db_data:
```

### 为知笔记

普通命令:

```bash
docker run --name wiz --restart=always -it -d -v  ~/wizdata:/wiz/storage -v  /etc/localtime:/etc/localtime -p 8081:80 -p 9269:9269/udp  wiznote/wizserver
```

compose.yaml

```yaml
services:
  wiz:
    image: wiznote/wizserver
    container_name: wiz
    tty: true
    stdin_open: true
    restart: always
    volumes:
      - ~/wizdata:/wiz/storage
      - /etc/localtime:/etc/localtime
    ports:
      - "8081:80"
      - "9269:9269/udp"
```

## 问题

### docker 命令中 -itd参数对应的 compose.yaml 中怎么写

在 Docker 命令中，-it 表示使用交互式终端并分配一个伪终端，-d 表示在后台运行容器。

对应的在 Compose 文件中，可以使用 tty 和 stdin_open 属性来实现 -it，docker-compose up时通过加-d 参数实现 -d，示例如下：

```yaml
services:
  my-service:
    image: ubuntu
    tty: true
    stdin_open: true
```

```bash
docker-compose up -d
```

