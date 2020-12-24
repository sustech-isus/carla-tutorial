# 基础知识

## CARLA
> 介绍CARLA的功能，特性，用途与宏观架构

### CARLA架构
> 介绍CARLA的宏观架构

### CARLA服务端
> CARLA Server的用途与背景（软件背景）

### CARLA客户端
> CARLA Client的用途与背景（软件背景）

## ROS
> 介绍ROS的基础功能

!> 对ROS的介绍不属于本文档的重点部分，关注点落在与协同仿真相关的内容上面

### 版本
> 推荐的版本，不使用其他版本的原因

### ROS Bridge
> 什么是ROS Bridge，在协同仿真中充当了什么样的角色

### ROS工具
> 本教程会提及的ROS工具如`rviz`的简单介绍

#### rviz

## 辅助工具
> 其他可能会用到的工具，如场景制作与建模（针对外包）

### RoadRunner
> 简单介绍软件功能，在仿真器系统中充当的角色

### Blender
> 简单介绍软件功能，在仿真器系统中充当的角色

# 安装环境

## 计算机硬件

### CPU 

Intel i7 9代-11代 / Intel i9 9代-11代/ AMD锐龙7/ AMD锐龙9

### 内存 
16GB RAM 及以上

### 显卡要求
NVIDIA RTX 2070 / NVIDIA RTX 2080 / NVIDIA RTX 3070 / NVIDIA RTX 3080
 
> **AMD显卡**：由于AMD对Ubuntu驱动支持不好，没办法在Ubuntu跑CARLA
> 
> **集显/核显/性能太差的独显**：会出现无法运行CARLA，严重掉帧等问题
>
> **部分性能略低于以上硬件要求的电脑也可以运行CARLA，请自行尝试**

## 操作系统

需要跑与ROS相关算法的请选择**Ubuntu 18.04**

只用到CARLA本体的可以选择**Ubuntu 18.04, Windows 10**

**本文档最后一章的演示用例所用的系统均为Ubuntu 18.04**
 
> 当前为 Ubuntu 18.04LTS，如果CARLA官方更新20.04LTS我们这边根据大家工作的情况调整，操作系统的安装教程，源配置（外部引用）

## Python

Python2.7或Python3.7

> Python 2.7和3.7可以直接使用官方提供的发行版CARLA，其他版本Python需要从源码自行编译CARLA，如果没有特殊需求**非常不建议**从源码自行编译CARLA

# CARLA安装与配置

**本篇文档以Ubuntu 18.04下安装CARLA 0.9.9为例**

## 本地运行

### 下载发行版CARLA

可以从南方科技大学内网下载发行版CARLA镜像：[SUSTC CARLA](http://cdn.isus.tech/%E5%B8%B8%E7%94%A8%E4%B8%8B%E8%BD%BD/carla/)，也可以从github CARLA发布界面[Github CARLA](https://github.com/carla-simulator/carla/blob/master/Docs/download.md)下载

![avatar](../../images/Carla_Github_Page.png)

根据操作系统下载对应的压缩包
> Linux系统为tar.gz结尾的压缩包，Windows系统为zip结尾的压缩包

![avatar](../../images/Carla_Github_Page2.png)



新建文件夹CARLA_0.9.9，将压缩包文件复制到该文件夹下，解压缩
```
mkdir ~/CARLA_0.9.9
cp <where is the package>/CARLA_0.9.9.4.tar.gz ~/CARLA_0.9.9/CARLA_0.9.9.4.tar.gz
cd ~/CARLA_0.9.9
tar -zxvf CARLA_0.9.9.4.tar.gz
```


### 启动CARLA服务端
切换到CARLA安装目录
```
cd ~/CARLA_0.9.9
```
启动CARLA服务端
```
./CarlaUE4.sh
```
![avatar](../../images/Carla_Local_Server.png)

### 启动CARLA客户端
本篇文档以python 2.7为例

查看python和pip版本是否均为2.7
```
python -V
pip -V
```
![avatar](../../images/Python_Path.png)

安装pygame和numpy两个python包
```
pip install --user pygame numpy
```

切换到CARLA安装目录, 启动键盘控制车辆的Python脚本manual_control.py

```
cd ~/CARLA_0.9.9/PythonAPI/examples
python manual_control.py
```
![avatar](../../images/Carla_Manual_Control.png)


## 联机运行
> 将CARLA Server与Client分别部署于两台物理机或者虚拟机，并完成手动控制小车移动为止

# ROS安装与配置

ROS有多个版本，分别对应不同的linux发行版,本篇文档以安装ROS Melodic为例。
> **ROS版本与Ubuntu版本对照**
> 
> * ROS Kinetic -> Ubuntu 16.04
> * ROS Melodic -> Ubuntu 18.04
> * ROS Noetic -> Ubuntu 20.04


### 配置sources.list

向sources.list中添加ROS源。
```
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
```

> 官方ROS源下载速度比较慢，这里换成了清华的镜像源。
> 
> 也可以替换其他镜像源: [Mirrors](http://wiki.ros.org/ROS/Installation/UbuntuMirrors)


### 添加密钥
```
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```
### 安装ROS
更新软件源
```
sudo apt update
```
安装完整版的ROS
```
sudo apt install ros-melodic-desktop-full
```
### 设置环境变量
```
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
### 安装构建ROS软件包所需的依赖

到目前为止，运行核心ROS软件包所需的软件已经安装完成了。 要创建和管理ROS工作区，需要安装其他依赖关系
```
sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
```

在使用许多ROS工具之前，需要初始化rosdep。 rosdep可以轻松地为要编译的源安装系统依赖性，同时rosdep也是ROS系统中某些核心组件运行所必须的。安装rosdep
```
sudo apt install python-rosdep
```
初始化rosdep
```
sudo rosdep init
rosdep update
```

### 测试ROS demo
运行roscore
```
roscore
```
若正常出现与以下内容近似的信息，说明已经成功安装
```
SUMMARY
========

PARAMETERS
 * /rosdistro: melodic
 * /rosversion: 1.14.9

NODES

auto-starting new master
process[master]: started with pid [4443]
ROS_MASTER_URI=http://sakamoto-PC:11311/

setting /run_id to 3a5836a2-eb3a-11ea-8edc-dcfb484d8811
process[rosout-1]: started with pid [4454]
started core service [/rosout]
```

新开一个terminal，运行以下命令，打开小乌龟窗口
```
rosrun turtlesim turtlesim_node
```
![avatar](../../images/ROS_Turtlesim.png)

新开一个terminal，运行以下命令，打开乌龟控制窗口，可使用方向键控制乌龟运动
```
rosrun turtlesim turtle_teleop_key
```
选中控制窗口的terminal，按方向键，可看到TurtleSim窗口中乌龟在运动。
![avatar](../../images/ROS_Turtlekey.png)

至此，ROS demo测试完成，说明ROS安装没有问题。

# 仿真器场景设置
> 选择地图，设置NPC车辆，天气系统，事故等

# 传感器与数据采集
> 设置车辆传感器，数据输出，整理，使用（感知）

## 基础方法

## 使用CARLA ROS


### 源码编译CARLA-ROS
本篇文档以CARLA 0.9.9和ROS Melodic为例

打开终端，建立CARLA-ROS文件夹结构
```
#setup folder structure
mkdir -p ~/carla-ros-bridge/catkin_ws/src
```
从github下载carla-ros-bridge的源码
```
cd ~/carla-ros-bridge
git clone -b 0.9.8 https://github.com/carla-simulator/ros-bridge.git
cd ros-bridge
git submodule update --init
cd ~/carla-ros-bridge/catkin_ws/src
ln -s ../../ros-bridge
source /opt/ros/melodic/setup.bash
cd ..

#install required ros-dependencies
rosdep update
rosdep install --from-paths src --ignore-src -r
```
![avatar](../../images/ROS_Update.png)

编译源码
```
cd ~/carla-ros-bridge/catkin_ws
catkin_make
```
![avatar](../../images/Catkin_Make.png)

编辑PYTHON路径，打开编辑器
```
gedit .bashrc
```
添加相对应的carla-python egg包，\<path-to-carla>请自行替换为CARLA安装路径，末尾添加
```
export PYTHONPATH=$PYTHONPATH:<path-to-carla>/PythonAPI/carla/dist/carla-0.9.9-py2.7-linux-x86_64.egg
source ~/carla-ros-bridge/catkin_ws/devel/setup.bash
```

如果有其他版本的CARLA-Python egg包路径请注释掉

### 3.2 测试CARLA-ROS Demo
新建终端，切换到CARLA安装目录，启动CARLA:
```
cd ~/CARLA_0.9.9
./CarlaUE4.sh
```

新建终端，运行手动控制车辆的demo
```
roslaunch carla_ros_bridge carla_ros_bridge_with_example_ego_vehicle.launch
```
> 这里的手动控制脚本有些不同，在pygame的窗口，先按B键启动手动控制，然后才能用键盘WASD控制车辆
> 
![avatar](../../images/Carla_ROS_Vehicle.png)

新建终端，可视化ros topic
```
rosrun rviz rviz
```
选择File-Open Config，打开`~/carla-ros-bridge/ros-bridge/carla_ros_bridge/config/carla_default_rviz.cfg.rviz`，在右侧Display窗口，在PointCloud2下Topic选择point_cloud即可生成点云图像，如果显示正确则demo运行正常
![avatar](../../images/Carla_ROS_Rviz.png)

![avatar](../../images/Carla_ROS_Rviz2.png)

> rviz左侧两个Image窗口没有图像的原因是，这两个Image对应的Topic分别是image_depth和image_segmentation，而默认的ego vehicle没有添加深度摄像机和语义摄像机的传感器

> ego_vehicle对应的sensor文件在/opt/carla-ros-bridge/melodic/share/carla_ego_vehicle/config/sensor.json，如需添加新的sensor，请参考[Sensors Reference](https://carla.readthedocs.io/en/latest/ref_sensors/)

# 控制车辆
> 使用代码进行基础的车辆控制（决策）

## 基础方法

## 使用CARLA ROS

# 演示用例

## Costmap
