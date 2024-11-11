# Docker
## 制作基础镜像
cd Dockerfile
docker build --no-cache -t ubuntu20.04:base ./  -f ./Dockerfile-base .

## 制作发布镜像

## 制作容器
根据code应用程序安装各种库，保证code编译运行成功，安装过程遇到的问题参看INSTALL.md

## 使用容器
- 启动容器  
  docker start be7732c79c82  

- 进入容器  
  docker exec -it be7732c79c82 /bin/bash 
 
- 修改DISPLAY环境变量  
  export DISPLAY=192.168.0.113:0.0  

- 编译运行code应用程序  
  cd code/build  
  cmake ../ && make 
  ./cv_crop_img
