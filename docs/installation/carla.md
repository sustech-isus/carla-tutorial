# CARLA的安装

本文档提供了三种CARLA的安装部署方式，请根据自己的需求选择最为适当的方式进行安装。请根据下面的引导选择您的安装方式。

1. 如果您有下列需求，请**务必**以[编译方式安装CARLA](#以编译方式安装CARLA)：

    * 使用自定义地图

    * 使用自定义车辆

    * 使用自定义的传感器模型

    * 使用除`python 2.7`或`python 3.7`以外的特别版本

2. 如果您处于下列情形之一，请以[安装包方式部署CARLA](#以安装包方式部署CARLA)：

    * 您是初学者，首次接触CARLA

    * 您使用非NVIDIA显卡

3. 如果您了解且熟悉Docker的操作，可以尝试以[Docker方式部署CARLA](#以Docker方式部署CARLA)

> [!TIP]
>
> 如果您不确定您的需求，我们强烈推荐以[包方式部署CARLA](#以安装包方式部署CARLA)

> [!NOTE]
> 
> 在Windows系统下CARLA的安装与编译不在本文档涉及的范围之内，请参考官方文档相关部分，详见
>
> [https://carla.readthedocs.io/en/latest/build_windows/](https://carla.readthedocs.io/en/latest/build_windows/)

## 以安装包方式部署CARLA

以下内容为以安装包方式部署CARLA的教程。

### 安装依赖
使用CARLA需要安装两个Python依赖包，请使用`pip`工具进行安装
```
pip install --user pygame numpy
```

> [!ATTENTION]
> 安装依赖前请根据文档[软件环境](./installation/software_environment.md)部分再次确认Python的版本

### 下载安装包

> [!NOTE]
> 本教程以 `CARLA 0.9.11` 版本为例

访问CARAL的Github Repositories中的[Release](https://github.com/carla-simulator/carla/releases/)页面，点击您所需要的版本下载并保存到本地。请同时下载`CARLR_{version).tar.gz`主程序文件与`AdditionalMaps_{version}.tar.gz`地图扩展包。

![avatar](../../images/installation/2.png)

----------
> [!TIP]
>
> 这是我们推荐的最佳下载方式

此外，我们提供了CARLA官方安装包在南科大校内网的镜像，推荐您从[该处](http://cdn.isus.tech/downloads/carla/)下载以获得更快的下载速度。

![avatar](../../images/installation/3.png)



---------

作为示例，我们将这两个压缩包储存于下述地址
```
~/Downloads/CARLA_0.9.11.tar.gz
~/Downloads/AdditionalMaps_0.9.11.tar.gz
```

![avatar](../../images/installation/1.png)

### 解压安装

建立用于存放CARLA应用程序的文件夹

```
$ mkdir -p ~/CARLA/0_9_11
```

> [!TIP]
> 我们推荐以文件夹的方式管理CARLA的不同版本，例如
> ```
> ├── CARLA
│   ├── 0_9_10
│   └── 0_9_11
> ```

-------------
将安装程序压缩包`CARLA_{version}.tar.gz`解压缩至刚刚创建的文件夹内

```
$ tar -zxvf ~/Downloads/CARLA_0.9.11.tar.gz -C ~/CARLA/0_9_11
```

可以通过访问文件夹或者`ll`命令检查解压结果是否正确

![avatar](../../images/installation/4.png)


-------------
接下来安装CARLA的附加资产包`AdditionalMaps_{version}.tar.gz`，将其直接解压缩至目标CARLA版本的文件夹下

```
$ tar -zxvf ~/Downloads/AdditionalMaps_0.9.11.tar.gz -C ~/CARLA/0_9_11
```

> [!WARNING]
> 请确保将附加资产包和CARLA主程序的版本一致

--------------

使用下列命令导入资产
```
$ cd ~/CARLA/0_9_11
$ ./ImportAssets.sh
```
如果您已经正确安装了`AdditionalMaps`附加资产包，这个命令应该会很快结束，如果您安装不正确，运行这个命令将会从云端拉取附加资产包。

### 运行与验证

首先启动CARLA的服务端，进入当前版本的应用程序根目录
```
$ cd ~/CARLA/0_9_11
```
启动CARLA服务端
```
$ ./CarlaUE4.sh
```
如果一切正常，您将会看到如下界面，这说明您的CARLA服务端已经正常启动

![avatar](../../images/installation/5.png)

-------------

接下来启动CARLA的客户端，进入当前版本的PythonAPI例程目录
```
$ cd ~/CARLA/0_9_11/PythonAPI/examples
```
启动客户端，在这里的例子为使用键盘控制车辆的Python脚本`manual_control.py`
```
$ python manual_control.py
```

如果一切正常，您将会看到如下界面，这说明您的CARLA客户端已经正常启动

![avatar](../../images/installation/6.png)

CARLA的安装到此结束。

## 以Docker方式部署CARLA

> [!NOTE]
> 
> 请参考官方文档相关部分，详见
>
> [https://carla.readthedocs.io/en/latest/build_docker/](https://carla.readthedocs.io/en/latest/build_docker/)

> [!TIP]
>
> 我们提供了南科大校内的Docker源，推荐您使用该Docker源进行进行安装，以获得更快的下载速度
>
> https://harbor.isus.tech/harbor/projects/3/repositories/carla

## 以编译方式安装CARLA

> [!NOTE]
> 
> 请参考官方文档相关部分，详见
>
> [https://carla.readthedocs.io/en/latest/build_linux/](https://carla.readthedocs.io/en/latest/build_linux/)
