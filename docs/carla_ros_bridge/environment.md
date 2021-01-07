# 仿真环境配置

本部分提供了Carla ROS-Bridge的基础环境配置流程。

## 安装并启动Carla服务端

若需要使用Carla ROS-Brige工程，需要先启动Carla Server服务端。

### 使用Release预编译版本

第一种启动服务端的方式是直接下载预编译的Carla服务端, 直接执行以下命令即可。

```bash
cd $CARLA_ROOT  #切换至CARLA文件夹
./CARLA_UE4.sh
```

> [!NOTE]
>
> 预编译版本下载及安装的详细流程可以参考 [CARLA的安装](/installation/carla) 部分。


第二种方式使用Docker版本服务端，更适合用于服务器等环境，默认关闭服务端可视化显示，并在后台持续运行。

### 使用Docker版本
```bash
# 以启动0.9.10.1版本为例
docker run -d --name=carla-server --ipc=host --network=host --runtime=nvidia --gpus all -e SDL_VIDEODRIVER=offscreen --restart=always harbor.isus.tech/carlasim/carla:0.9.10.1 bash CarlaUE4.sh

```
|            **参数**            |       **说明**       |
| :----------------------------: | :------------------: |
|              `-d`              | 后台运行容器 |
|            `--name=carla-server`  | 指定容器名称为`carla-server`
|          `--network`           | 指定容器网络连接类型为`host`模式，与宿主机使用相同的网络
|          `--runtime=nvidia --gpus all`          | 启用nvidia-docker, 映射全部显卡
| `-e SDL_VIDEODRIVER=offscreen` | 添加环境变量，禁用服务端GUI界面
|       `--restart=always`       |  自动重新启动

> [!NOTE]
>
> `harbor.isus.tech`为内网容器仓库，若使用公网Docker Hub, 可以直接使用 `carlasim/carla:相应版本`

## 配置并编译 ROS Bridge代码

```bash
# 创建workspace，并拉取ROS Bridge代码
mkdir -p ~/carla_ros_ws/src
cd ~/carla_ros_ws/src
git clone https://github.com/carla-simulator/ros-bridge.git -b 0.9.10.1
cd ros-bridge

# 拉取submodule
git submodule update --init

cd ~/carla_ros_ws
# 利用rosdep工具安装相关依赖
rosdep update
rosdep install -y --from-paths src --ignore-src --rosdistro melodic

# 编译工程
catkin_make
# 加载环境变量
source devel/setup.bash
```

## 启动 ROS Bridge

```bash

export PYTHONPATH=$PYTHONPATH:<path-to-carla>/PythonAPI/carla/dist/carla-<carla_version_and_arch>.egg
source ~/carla_ros_ws/devel/setup.bash

roslaunch carla_ros_bridge carla_ros_bridge_with_example_ego_vehicle.launch

```


