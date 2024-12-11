## Docker配置

- 设置镜像加速, 设置私有仓库地址  
/etc/docker/daemon.json改成这个内容  
sudo systemctl daemon-reload  
sudo systemctl restart docker  
```
{
    "registry-mirrors": [
        "https://do.nark.eu.org",
        "https://dc.j8.work",
        "https://docker.m.daocloud.io",
        "https://dockerproxy.com",
        "https://docker.mirrors.ustc.edu.cn",
        "https://docker.nju.edu.cn",
        "https://zbi3ynx1.mirror.aliyuncs.com"
    ],                                                                                                                                                                                                                                                                     
    "insecure-registries":["192.168.70.202:32373", "192.168.70.201:32373", "192.168.68.102"]
}
```

## Docker 基础命令

- 查看镜像   
docker images

- 删除镜像  
docker rmi IMAGE_ID

- 标记镜像  
docker tag IMAGE_ID IMAGE_NAME:TAG

- 导出镜像  
docker save -o ubuntu_20.04_vim.tar IMAGE_ID  

- 加载镜像  
docker load --input ubuntu_20.04_vim.tar

- 查看所有容器  
docker ps -a  

- 从镜像启动容器  
docker run -i -t ubuntu:20.04 /bin/bash // 交互式登陆，-t 新建一个终端，-i 允许标准输入； 
docker run -v /home/lc/work/slam_oncloud:/home -it 192.168.70.202:32373/registry/mgs/cloud/slamoncloud:mgs_base_lc /bin/bash

```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]  
-d: 后台运行容器并返回容器 ID。  
-it: 交互式运行容器，分配一个伪终端。  
--name: 给容器指定一个名称。  
-p: 端口映射，格式为 host_port:container_port。  
-v: 挂载卷，格式为 host_dir:container_dir。  
--rm: 容器停止后自动删除容器。  
--env 或 -e: 设置环境变量。  
--network: 指定容器的网络模式。  
--restart: 容器的重启策略（如 no、on-failure、always、unless-stopped）。  
-u: 指定用户。
```  
- 启动容器  
sudo docker start CONTAINER_ID  

- 停止容器  
sudo docker stop CONTAINER_ID  

- 重启容器  
sudo docker restart CONTAINER_ID  

- 进入容器    
sudo docker attach CONTAINER_ID // 退出容器终端，容器终止  
sudo docker exec -it CONTAINER_ID /bin/bash // 退出容器终端，不会导致容器停止  

- 删除指定容器  
docker rm CONTAINER_ID  

- 导出容器快照 - (不包括 Docker 镜像的历史信息、环境变量、元数据等)  
sudo docker export CONTAINER_ID > hello_world.tar  

- 导入容器  
sudo docker import hello_world.tar my_new_image:latest

- 容器重命名
sudo docker rename old-container new-container 

- 导出容器为新的镜像  
docker commit -m "has update" -a "lc" 30bd86fa9c1b image:v3   
```
docker commit [OPTIONS] CONTAINER_ID [REPOSITORY[:TAG]]  
[REPOSITORY[:TAG]]：可选，指定新镜像的仓库名称和标签（如果未指定，Docker 会自动生成一个镜像 ID）。  
-a 或 --author：指定镜像的作者信息。  
-m 或 --message：为镜像添加提交信息，描述该次更改内容。  
-p 或 --pause：在提交过程中暂停容器（默认开启）。如果你不想暂停容器，可以将该选项设置为 false。  
```
- 查看容器LOG  
docker logs CONTAINER_ID 

- 清理所有停止状态的容器  
docker container prune  

- 拷贝文件  
```
docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH  
docker cp [OPTIONS] SRC_PATH CONTAINER:DEST_PATH  
-L: 如果源路径中包含符号链接，使用此参数会使 docker cp 跟随符号链接复制实际文件，而不是复制符号链接本身。  
```
- Dockfile创建镜像  
docker build -t IMAGE:TAG ./  
docker build --no-cache --build-arg REGISTRY=192.168.70.202:32373/registry -t 192.168.70.202:32373/registry/mgs/cloud/slamoncloud:mgs_deploy_lc -f ./docker/Dockerfile .  
```
-t, --tag: 用于为镜像命名并打标签，格式为 name:tag
-f, --file: 指定 Dockerfile 文件的路径，如果不在当前目录，指定相对或绝对路径
--no-cache: 禁用缓存，从头开始构建镜像，不使用之前的构建层
--build-arg: 构建时传入的变量，可用于 Dockerfile 内部的 ARG 指令
--output: 指定构建输出位置，例如将镜像导出到本地文件而不是加载到 Docker
    docker build --output type=local,dest=./out .
./ : 构建上下文所在的路径
```
FROM    定制镜像的Base  
RUN     执行命令分为 shell 格式和 exec 格式  
    RUN <命令行命令>                         RUN apt update  
    RUN ["可执行文件", "参数1", "参数2"]      RUN ["./test.php", "dev", "offline"]  
FROM- 镜像从那里来
MAINTAINER- 镜像维护者信息
RUN- 构建镜像执行的命令，每一次RUN都会构建一层  
CMD- 容器启动的命令，如果有多个则以最后一个为准，也可以为ENTRYPOINT提供参数  
VOLUME- 定义数据卷，如果没有定义则使用默认  
USER- 指定后续执行的用户组和用户  
WORKDIR- 切换当前执行的工作目录  
HEALTHCHECH- 健康检测指令  
ARG- 变量属性值，但不在容器内部起作用  
EXPOSE- 暴露端口  
ENV- 变量属性值，容器内部也会起作用  
ADD- 添加文件，如果是压缩文件也解压  
COPY- 添加文件，以复制的形式  
ENTRYPOINT- 容器进入时执行的命令
```
- docker pull 与 docker push
docker pull uhub.service.ucloud.cn/backup_images/ubuntu:20.04  
docker push 192.168.70.202:32373/registry/mgs/cloud/slamoncloud:mgs_base_lc  
