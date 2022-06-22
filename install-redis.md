# Install Redis - Docker Commad

搜索Reis镜像，这里展示的是官方最新的镜像</tr>`docker search redis`

使用官方[dockerhub](https://hub.docker.com/)搜索redis

选用常用的redis5.0作为安装的版本</tr>`docker pull redis:5.0`

不映射外部配置文件直接运行redis5.0镜像</tr>`docker run --name redis5 redis:5.0`

下载redis5.0版本的配置文件</tr>`wget https://raw.githubusercontent.com/redis/redis/5.0/redis.conf`

如果准备暴露在公网中，修改redis.conf的监听地址为`bind 0.0.0.0`.然后**一定要设置redis的密码** `requirepass xxx`

映射容器外配置文件运行redis5.0镜像</tr>
```shell
docker run -d \
            --privileged=true \
            -p 6379:6379 \
            -v /usr/local/etc/redis/redis.conf:/etc/redis/redis.conf \
            --name redis5 \
            redis:5.0 \
            redis-server /etc/redis/redis.conf
            
-d:表示后台静默运行
--privileged=true 表示给予容器中root账户真正的root权限，否则容器内root账户相对于宿主机而言只是一个普通用户
-p 宿主机端口：容器内端口 表示映射容器内端口到宿主机端口
-v 宿主机目录：容器内目录 表示映射宿主机的目录至容器内的目录
--name 表示指定当前启动的容器的名称，不指定的docker会随机生成一个容器名称。
redis:5.0 表示运行的镜像名称
redis-server /etc/redis/redis.conf 相当于Dockerfile中的CMD，表示容器启动之后运行的指令，这里是指定配置文件启动redis-server
```

使用`docker ps`查看容器是否启动成功。

如果没有正在运行中的容器，使用`docker logs redis5` 查看启动日志

使用 `docker exec --it redis5 /bin/bash`</tr>进入到容器中

使用 `docker exec --it redis5 redis-cli -a password`</tr>直接进入到redis-cli

使用 `docker stop redis5` 停止容器运行

使用 `docker rm redis5` 删除容器

使用 `docker rm -f redis5` 强制删除容器

---

当前是使用 docker 指令的方式一步一步的安装 redis，后续会提供使用 Dockerfile 构建镜像运行的方式。
