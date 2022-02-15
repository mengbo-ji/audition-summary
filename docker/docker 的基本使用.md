#  docker 基本使用入门



![img](https://gitee.com/AllenJoker/picgoimage/raw/master/img/docker01.png)

> Docker 是一个开源的应用容器引擎，基于 Go 语言并遵从 Apache2.0 协议开源。
>
> Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

## Docker的应用场景

- Web 应用的自动化打包和发布。
- 自动化测试和持续集成、发布。
- 在服务型环境中部署和调整数据库或其他的后台应用。
- 从头编译或者扩展现有的 OpenShift 或 Cloud Foundry 平台来搭建自己的 PaaS 环境。

# Docker 架构

Docker 包括三个基本概念:

- **镜像（Image）**：Docker 镜像（Image），就相当于是一个 root 文件系统。比如官方镜像 ubuntu:16.04 就包含了完整的一套 Ubuntu16.04 最小系统的 root 文件系统。
- **容器（Container）**：镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。
- **仓库（Repository）**：仓库可看成一个代码控制中心，用来保存镜像。



## 基本命令

### search

````bash
docker search nginx
````

### image

````bash
 docker images
````

### pull

````bash
docker pull hello-world
````

### run

````bash
# -d 后台运行
# -p 端口映射 
docker run -d -p 8080:80 nginx
````

````bash
alanallen@localhost> ~ docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
````

<img src="https://gitee.com/AllenJoker/picgoimage/raw/master/img/image-20211223124420618.png" style="zoom: 50%;" />

### ps

````bash
# 查看当前运行的容器
docker ps
# -a :显示所有的容器，包括未运行的
docker ps -a
````

### exec

````bash
docker exec --help
# -i :即使没有附加也保持STDIN 打开
# -t :分配一个伪终端
docker exec -it  aca35a0af913 bash
````

### stop

````bash
docker stop container_id
````

### start

````bash
docker start container_id
````

### build

````bash
docker build . your_images:tags
````

### create 

````bash
docker create  --name my_nginx  nginx:latest      
````

### rm

- **-f :**通过 SIGKILL 信号强制删除一个运行中的容器。
- **-l :**移除容器间的网络连接，而非容器本身。
- **-v :**删除与容器关联的卷。

````bash
# 强制删除
docker rm -f my_nginx

# 移除容器 my_nginx 对容器 db01 的连接，连接名 db
docker rm -l db01

# 删除容器 my_nginx, 并删除容器挂载的数据卷
docker rm -v my_nginx

# 删除所有已经停止的容器
docker rm $(docker ps -a -q)
````



### rmi

````bash
# -f :强制删除
docker rmi -f nginx:latest
````

### logs

- **-f :** 跟踪日志输出
- **--since :**显示某个开始时间的所有日志
- **-t :** 显示时间戳
- **--tail :**仅列出最新N条容器日志

````bash
docker logs -f my_nginx
# 查看容器mynginx从2021-12-21后的最新10条日志
docker logs --since="2021-12-21" --tail=10 my_nginx
````

### inspect

> 获取容器/镜像的元数据

````bash
docker inspect nginx

[
    {
        "Id": "sha256:fc16ec0c2d9106ce8da4a20e39c2a8dca83aed0f3b14ef6ae68ac91eda3a5c53",
        "RepoTags": [
            "nginx:latest"
        ],
        "RepoDigests": [
            "nginx@sha256:366e9f1ddebdb844044c2fafd13b75271a9f620819370f8971220c2b330a9254"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2021-12-21T02:46:53.262860559Z",
        "Container": "543e5d05cc3268d3fba2542c34c5267c2d69c0c2bb554eea954399f70995386d",
        "ContainerConfig": {
            "Hostname": "543e5d05cc32",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.21.4",
                "NJS_VERSION=0.7.0",
                "PKG_RELEASE=1~bullseye"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"nginx\" \"-g\" \"daemon off;\"]"
            ],
            "Image": "sha256:bc5ea8ba87a69381a1222ee9d7819dceab5ebf461b48ef52192c1b340d587962",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "DockerVersion": "20.10.7",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.21.4",
                "NJS_VERSION=0.7.0",
                "PKG_RELEASE=1~bullseye"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "sha256:bc5ea8ba87a69381a1222ee9d7819dceab5ebf461b48ef52192c1b340d587962",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "Architecture": "arm64",
        "Variant": "v8",
        "Os": "linux",
        "Size": 134454429,
        "VirtualSize": 134454429,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/7fc86e5adf2ec57a60dc4df1b807ad4db060262ac3f0607fe78f8f7a2b0d71a0/diff:/var/lib/docker/overlay2/24e24f379437450cb95aeffd0b3b7d6a12fd40aea218971964fc54b3a47dfc53/diff:/var/lib/docker/overlay2/9f701b196348b68a0484d0e81f0ea1b3bfa62bfec532d19f9281344a4b8d0930/diff:/var/lib/docker/overlay2/1412a39909997fbd5445ef923f4b6d3fdc95a16d79f75b539701f2e0989876e3/diff:/var/lib/docker/overlay2/0511a4b9f774bb73e8c6d09230e9f01792183ab0626c229e8cf268dfacff9cc7/diff",
                "MergedDir": "/var/lib/docker/overlay2/59a2b2245e385c2d510c9c6510a7ba6fe95117630b5fe2f3a55a3d11e5d50283/merged",
                "UpperDir": "/var/lib/docker/overlay2/59a2b2245e385c2d510c9c6510a7ba6fe95117630b5fe2f3a55a3d11e5d50283/diff",
                "WorkDir": "/var/lib/docker/overlay2/59a2b2245e385c2d510c9c6510a7ba6fe95117630b5fe2f3a55a3d11e5d50283/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:1c79be3b9cebb9838b5c607567cb18eb50cd94e39b20a6241ca7d2d53dcffc89",
                "sha256:14094e49edd4a92c3fda06c84f2f1356751572b7c5fa3c9fe3f805874abeede9",
                "sha256:73aad438cb2851ca163618f92bec4e849a89cf9f67b2b348efff46179cd16e6e",
                "sha256:8bd5bd3f7acb19ff37217771b6f97fc43c470637d7ebe0d7d4e300b0e222d8f4",
                "sha256:c1faa131c3402b2f1e3c12996a2fa8bbfb344a18c6a9d157632f1f85a63804ab",
                "sha256:c92f511a5cc24659fb8b6784dd667e8e2296e1514be70ea1b479d806a9926fc4"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
````

## Dockerfile

| command    | explain                                                      |
| ---------- | ------------------------------------------------------------ |
| FROM       | base image                                                   |
| RUN        | 执行命令并创建新的镜像层，RUN 经常用于安装软件包             |
| ADD        | 添加文件 (可以添加远程文件)                                  |
| COPY       | 复制到容器指定的目录下                                       |
| CMD        | 设置容器启动后默认执行的命令及其参数，但 CMD 能够被 `docker run` 后面跟的命令行参数替换<br/>也可用于给 ENTRYPOINT传递参数 |
| ENTRYPOINT | ENTRYPOINT 容器启动后执行的命令,让容器执行表现的像一个可执行程序一样,与CMD 的 区 别 是 不 可 以 被 docker run 覆 盖 , 会 把 docker run 后 面 的 参 数 当 作 传 递 给<br/>ENTRYPOINT 指令的参数。<br/>Dockerfile 中只能指定一个 ENTRYPOINT,如果指定了很多,只 有 最 后 一 个 有 效 。<br/>docker run 命 令 的 -entrypoint 参 数 可 以 把 指 定 的 参 数 继 续 传 递 给ENTRYPOINT |
| EXPOSE     | 暴露端口                                                     |
| WORKDIR    | 指定路径                                                     |
| MAINTAINER | 作者                                                         |
| ENV        | 环境变量                                                     |
| USER       | 指定操作用户, 一般不是 root                                  |
| VOLUME     | 容器所挂载的卷                                               |

> **镜像分层**
>
> Dockerfile 的指令每执行一次都会在 docker 上新建一层。所以过多无意义的层，会造成镜像膨胀过大.
>
> 在不同镜像中 分层可以共享
>
> 如下，以 **&&** 符号连接命令，这样执行后，只会创建 1 层镜像

````dockerfile
FROM centos
RUN yum -y install wget \
    && wget -O redis.tar.gz "http://download.redis.io/releases/redis-5.0.3.tar.gz" \
    && tar -xvf redis.tar.gz
````

### volume 操作

1. 通过 run -v $local_dir:$docker_dir 

````bash 
docker run -v $pwd/code:var/www/html nginx
````

2. 容器之间共享挂载卷

````bash
docker create -v $PWD/data:$var/data --name data_container ubuntu

docker run -it -volumes-from data_container ubuntu /bin/bash
root@container_id:/# cd /var/data 
root@container_id:/var/data# ls
root@container_id:/var/data# touch helloworld.txt
root@container_id:/var/data# exit
ls $PWD/data
helloworld.txt
````



## 镜像中心 Registry

### 1. 登录阿里云容器镜像服务, 按照提示创建个人实例

关于加速器的地址，您登录[容器镜像服务控制台](https://cr.console.aliyun.com/)后，在左侧导航栏选择 **镜像工具 >镜像加速器**，在**镜像加速器**页面就会显示为您独立分配的加速器地址。

```bash
例如：
加速器地址：https://[系统分配前缀].mirror.aliyuncs.com    
```

### 2. 镜像加速

在任务栏点击 Docker Desktop 应用图标 -> Perferences，在左侧导航菜单选择 Docker Engine，在右侧输入栏编辑 json 文件。将

`https://[系统分配前缀].mirror.aliyuncs.com` 加到"registry-mirrors"的数组里，点击 Apply & Restart按钮，等待Docker重启并应用配置的镜像加速器。

![](https://gitee.com/AllenJoker/picgoimage/raw/master/img/image-20211223143225843.png)

### 3. 验证

````bash
docker info | grep -A 1  "Registry Mirrors"
````

![](https://gitee.com/AllenJoker/picgoimage/raw/master/img/image-20211223143717584.png)
