# docker-compose 使用教程

> Compose 是用于定义和运行多容器 Docker 应用程序的工具。通过 Compose，您可以使用 YML 文件来配置应用程序需要的所有服务。然后，使用一个命令，就可以从 YML 文件配置中创建并启动所有服务。

#### Compose 使用的三个步骤：

- 使用 Dockerfile 定义应用程序的环境。
- 使用 docker-compose.yml 定义构成应用程序的服务，这样它们可以在隔离环境中一起运行。
- 最后，执行 docker-compose up 命令来启动并运行整个应用程序。

> Ghost 是一个免费开源博客平台, 接下来我们将以 Ghost 为例, 使用 docker-compose 来部署一个 Ghost 博客平台. 
>
> 笔者使用的 Mac 是 m1芯片 , mysql 只有  MySQL Server 8.0 以上的版本 适用于 x86 和 AArch64(ARM64) 架构. 所以我们将使用 
>
> ghost , nginx 和 mysql/mysql-server 镜像来搭建我们的博客平台.

### 创建 Docker Compose 文件

1. 创建并切换到一个目录来保存新的 Docker Compose 服务：

   ```bash
   mkdir blogs && cd blogs
   ```

   创建如下目录:

   ````bash
   blogs
   ├── docker-compose.yml
   ├── ghost_content
   ├── mysql
   │   ├── conf
   │   ├── data
   │   └── init
   └── nginx
       ├── Dockerfile
       └── nginx.conf
   ````

2. 构建 ghost 对外挂载卷 

   ````bash
   mkdir ghost_content
   ````

3. 创建 nginx 目录并添加相关配置

   ````bash
   mkdir nginx
   vim nginx/nginx.conf
   # nginx.conf
   worker_processes 4;
   events {worker_connections 1024;}
   http {
       server{
           listen 80;
           location / {
               proxy_pass http://ghost:2368;
           }
       }
   }
   ````

   ````dockerfile
   vim nginx/Dockerfile
   # Dockerfile
   FROM nginx
   COPY nginx.conf /etc/nginx/nginx.conf
   EXPOSE 80
   ````

4. 创建 mysql 挂载卷

   ````bash
   mkdir mysql/conf mysql/data mysql/init
   ````

5. 创建一个名为的文件`docker-compose.yml`

   ````bash
   vim docker-compose.yml
   ````

   ````yaml
   version: '3.1'
   
   services:
     ghost:
       image: ghost
       ports:
          - 2368:2368
       restart: unless-stopped
       environment:
         database__client: mysql
         database__connection__host: db
         database__connection__user: ghost
         database__connection__password: ghost
         database__connection__database: ghost
         url: http://localhost:2368
       volumes:
         - $PWD/ghost_content:/var/lib/ghost/content
   
     nginx:
       build: nginx
       depends_on:
         - ghost
       restart: unless-stopped
       ports:
         - 80:80
   
     db:
       image: mysql/mysql-server
       environment:
         MYSQL_ROOT_PASSWORD: ghost
         MYSQL_DATABASE: ghost
         MYSQL_USER: ghost
         MYSQL_PASSWORD: ghost
       command:
         --default-authentication-plugin=mysql_native_password
       volumes:
         - $PWD/mysql/data/:/var/lib/mysql/
         - $PWD/mysql/conf/:/etc/mysql/conf.d/
         - $PWD/mysql/init/:/docker-entrypoint-initdb.d/
       ports:
         - 3306:3306
   
   ````

   

### 运行和测试ghost 服务

`ghost`通过运行`docker-compose.yml`文件中定义的所有服务，从目录启动 Ghost CMS ：

```bash
docker-compose up -d --build
```

关闭你的容器：

```bash
cd blogs
docker-compose down
```

其他操作

````bash
# 停掉所有的容器
docer-compose stop

# 删除所有的容器
docker-compose rm

# 已有容器时的重新构建
docker-compose build
````

## 设置 ghost

访问 http://localhost/ghost

![image-20211224144057656](https://gitee.com/AllenJoker/picgoimage/raw/master/img/image-20211224144057656.png)

![image-20211224143214012](https://gitee.com/AllenJoker/picgoimage/raw/master/img/image-20211224143214012.png)

![](https://gitee.com/AllenJoker/picgoimage/raw/master/img/image-20211224144156676.png)

![image-20211224144029710](https://gitee.com/AllenJoker/picgoimage/raw/master/img/image-20211224144029710.png)



## docker-compose.yml 相关解释

### version

指定本 yml 依从的 compose 哪个版本制定的。

### build

指定为构建镜像上下文路径：

例如 webapp 服务，指定为从上下文路径 ./dir/Dockerfile 所构建的镜像：

````yaml
version: "3.7"
services:
  webapp:
    build: ./dir
````

或者，作为具有在上下文指定的路径的对象，以及可选的 Dockerfile 和 args：

```yaml
version: "3.7"
services:
  webapp:
    build:
      context: ./dir
      dockerfile: Dockerfile-alternate
      args:
        buildno: 1
      labels:
        - "com.example.description=Accounting webapp"
        - "com.example.department=Finance"
        - "com.example.label-with-empty-value"
      target: prod
```

- context：上下文路径。
- dockerfile：指定构建镜像的 Dockerfile 文件名。
- args：添加构建参数，这是只能在构建过程中访问的环境变量。
- labels：设置构建镜像的标签。
- target：多层构建，可以指定构建哪一层。

### depends_on

设置依赖关系。

- docker-compose up ：以依赖性顺序启动服务。在以下示例中，先启动 db 和 redis ，才会启动 web。
- docker-compose up SERVICE ：自动包含 SERVICE 的依赖项。在以下示例中，docker-compose up web 还将创建并启动 db 和 redis。
- docker-compose stop ：按依赖关系顺序停止服务。在以下示例中，web 在 db 和 redis 之前停止。

```
version: "3.7"
services:
  web:
    build: .
    depends_on:
      - db
      - redis
  redis:
    image: redis
  db:
    image: postgres
```

注意：web 服务不会等待 redis db 完全启动 之后才启动。

### entrypoint

覆盖容器默认的 entrypoint。

```
entrypoint: /code/entrypoint.sh
```

也可以是以下格式：

```yaml
entrypoint:
    - php
    - -d
    - zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20100525/xdebug.so
    - -d
    - memory_limit=-1
    - vendor/bin/phpunit
```

### environment

添加环境变量。您可以使用数组或字典、任何布尔值，布尔值需要用引号引起来，以确保 YML 解析器不会将其转换为 True 或 False。

```yaml
environment:
  RACK_ENV: development
  SHOW: 'true'
```

### expose

暴露端口，但不映射到宿主机，只被连接的服务访问。

仅可以指定内部端口为参数：

```yaml
expose:
 - "3000"
 - "8000"
```

### image

指定容器运行的镜像。以下格式都可以：

```yaml
image: redis
image: ubuntu:14.04
image: tutum/influxdb
image: example-registry.com:4000/postgresql
image: a4bc65fd # 镜像id
```

### networks

配置容器连接的网络，引用顶级 networks 下的条目 。

```
services:
  some-service:
    networks:
      some-network:
        aliases:
         - alias1
      other-network:
        aliases:
         - alias2
networks:
  some-network:
    # Use a custom driver
    driver: custom-driver-1
  other-network:
    # Use a custom driver which takes special options
    driver: custom-driver-2
```

**aliases** ：同一网络上的其他容器可以使用服务名称或此别名来连接到对应容器的服务。

### restart

- no：是默认的重启策略，在任何情况下都不会重启容器。
- always：容器总是重新启动。
- on-failure：在容器非正常退出时（退出状态非0），才会重启容器。
- unless-stopped：在容器退出时总是重启容器，但是不考虑在Docker守护进程启动时就已经停止了的容器

```yaml
restart: no
restart: always
restart: on-failure
restart: unless-stopped
```

注：swarm 集群模式，请改用 restart_policy。

### command

覆盖容器启动的默认命令。

```yaml
command: ["bundle", "exec", "thin", "-p", "3000"]
```

### volumes

将主机的数据卷或着文件挂载到容器里。

```yaml
version: "3.7"
services:
  db:
    image: postgres:latest
    volumes:
      - "/localhost/postgres.sock:/var/run/postgres/postgres.sock"
      - "/localhost/data:/var/lib/postgresql/data"
```