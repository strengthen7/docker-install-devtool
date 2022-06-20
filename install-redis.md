# Install Redis

搜索Reis镜像，这里展示的是官方最新的镜像</tr>`docker search redis`

使用官方[dockerhub](https://hub.docker.com/)搜索redis

选用常用的redis5.0作为安装的版本</tr>`docker pull redis:5.0`

不映射外部配置文件直接运行redis5.0镜像</tr>`docker run --name redis5 redis:5.0`

使用`docker ps`查看容器是否启动成功。

如果没有正在运行中的容器，使用`docker logs redis5` 查看启动日志

使用 `docker stop redis5` 停止容器运行

使用 `docker rm redis5` 删除容器

使用 `docker rm -f redis5` 强制删除容器
