### 高版本CMake
    wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | apt-key add -
    apt install software-properties-common
    apt-add-repository 'deb https://apt.kitware.com/ubuntu/ bionic main'
    apt-get update
    apt-get install cmake

### Eigen
    sudo apt-get install libeigen3-dev

    vim /usr/include/eigen3/Eigen/src/Core/util/Macros.h
        #define EIGEN_WORLD_VERSION 3
        #define EIGEN_MAJOR_VERSION 3
        #define EIGEN_MINOR_VERSION 7
---

### OpenCV
    sudo apt-get install libopencv-dev

    pkg-config --modversion opencv4
    4.2.0

    手动安装：
        sudo apt install libgtk2.0-dev

        mkdir build
        cd build
        cmake -D CMAKE_BUILD_TYPE=RELEASE \
        -D WITH_GTK=ON -D WITH_GTK_2_X=ON \
        -D OPENCV_ENABLE_NONFREE=ON \
        -D CMAKE_INSTALL_PREFIX=/usr \
        -D INSTALL_C_EXAMPLES=ON \
        -D INSTALL_PYTHON_EXAMPLES=ON \
        -D OPENCV_GENERATE_PKGCONFIG=ON \
        -D OPENCV_EXTRA_MODULES_PATH=/home/lc/work/package/opencv_contrib/modules \
        -D BUILD_EXAMPLES=ON ..
        make -j8
        sudo make install
---

### Geographic
    git clone https://github.com/geographiclib/geographiclib.git
    mkdir build && cd build
    cmake ../ && make -j8
    sudo make install
---

### Ceres
    sudo apt-get install libceres-dev

    vim /usr/include/ceres/version.h
        #define CERES_VERSION_MAJOR 1
        #define CERES_VERSION_MINOR 14
        #define CERES_VERSION_REVISION 0
---

### fmt
    git clone https://github.com/fmtlib/fmt.git
    git reset --hard 573d74395b3b0e745ea8c8de6bb7cde2bbade96a

    mkdir build && cd build
    cmake ../ && make -j8
    sudo make install
---

### Sophus
    git clone https://github.com/strasdat/Sophus.git
    git reset --hard d270df2be6e46501b1e7efc09b107517e0be0645

    mkdir build && cd build
    cmake ../ && make -j8
    sudo make install
---

### G2O
    git clone git@github.com:RainerKuemmerle/g2o.git
    
    git tag
    git show 20200410_git
    git reset --hard 6759465171a21087b47c246b611ab0aa19bd3be6
    
    mkdir build && cd build
    cmake ../ && make -j8 
    sudo make install

    Cholmod求解器相关使用apt安装：sudo apt install libsuitesparse-dev
---

### PCL
    sudo apt-get install libpcl-dev
   
    mkdir build
    cd build
    cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr ..
    make -j8
    sudo make install

    dpkg -s libpcl-dev | grep Version
	Version: 1.10.0+dfsg-5ubuntu1

    卸载:
     sudo rm -rf /usr/include/pcl-1.13/ /usr/lib/libpcl* /usr/share/pcl-1.13/ /usr/bin/pcl* /usr/lib/x86_64-linux-gnu/libpcl*
    
     sudo apt-get install libpcl-conversions-dev
---

### ROS
    // 设置安装源
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
    sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.ustc.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
    
    // 设置Key
    sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

    // 安装
    sudo apt update
    sudo apt install ros-noetic-desktop-full

    // 配置环境变量
    echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
    source ~/.bashrc

    // 卸载
    sudo apt remove ros-noetic-*

    // 参考资料
    http://www.autolabor.com.cn/book/ROSTutorials/chapter1/12-roskai-fa-gong-ju-an-zhuang/124-an-zhuang-ros.html

### Protobuf
    curl -OL https://github.com/protocolbuffers/protobuf/releases/download/v3.19.6/protobuf-all-3.19.6.tar.gz

    ./configure --prefix=/usr
    make
    make install
    ldconfig

### CloudCompare
    cd build/
    cmake -DPLUGIN_STANDARD_QPCL=ON ../
    make -j 4
    sudo make install
 ---

### Python 3.10
    sudo ./configure --enable-optimizations --prefix=/usr
    sudo make j 8
    sudo make -j 8
    sudo make install
    python3.10 --version

--- 
### docker 启动
    主机安装Xming将Xserver启动后，再将容器内显示连接到主机的Xserver上, docker 启动命令参考如下：
    sudo docker run -v /mnt/d/work:/workspace -it ubuntu_20.04:base -e DISPLAY=172.21.176.10:0.0 /bin/bash  

### apt 安装
    libyaml-cpp-dev
