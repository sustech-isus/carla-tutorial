# Introduction | 介绍
This is a project at HAO's lab, SUSTech, to create a quick guide about how to use CARLA.
It inculdes:
* CARLA quick installization and configuration
* ROS quick installization and configuration
* Setup simulation scene and enviroment
* Ego vehicle basic sensor setting and data output
* Ego vehicle basic setting and control
* Use CARLA to generate dataset
* Use CARLA and ROS to deploy co-simulation

本项目由南方科技大学郝祁教授课题组建立，旨在提供CARLA自动驾驶仿真器的快速上手教程。
本文档包括：
* CARLA快速安装与配置
* ROS快速安装与配置
* 设置仿真器的场景与环境
* 受控车辆基础传感器配置与数据输出
* 受控车辆基础控制
* 使用CARLA生成数据集
* 使用CARLA和ROS进行联合仿真

# Release | 发布
The current release of the document can be found at the following address.

本教程最新的发布版可以在下列地址找到.

[English Document](https://zhao-zirui.github.io/CARLAQuickGuide/#/en/us) | [中文文档](https://zhao-zirui.github.io/CARLAQuickGuide/#/zh-cn/)

# Edit Rules ｜ 编写规范
This section includes constraints on the documentation specification.

本部分包括了对文档编写规范的约束。

## Structure | 文件结构

```
CARLAQuickStart
├── demo                // => Demo codes | 演示用代码
├── docs
│   ├── README.md       // => Current page ｜ 当前页面
│   ├── en-us
│   │   └── README.md   // => English document ｜ 英文文档
│   ├── index.html      // => Website docsify configuration ｜ 网页配置文件
│   └── zh-cn
│       └── README.md   // => Chinese document ｜ 中文文档
└── images              // => Images storage | 图片储存
```
!> Do not modify the file structure or `index.html`, which will result in a publish page exception.

!> 不要修改文件结构与`index.html`，这将会导致发布页面异常

## Notice and Warning | 提示与警告
The following rules apply to the use of notice and warnings. Please pay attention to them when writing documents.

对提示与警告的使用做出如下规定，请在编写文档时注意。

> Notice, used for error and shortcut handling

> 提示，用作错误与捷径处理

!> Warning, used to indicate that an action may raise an error

!> 警告，用作提示操作可能引发错误

?> Hints, functional descriptions or other situations that are not necessary

?> 提示，功能说明或其他非必要说明的情况

## Push and Release | 上传与发布
This document is automatically published using The Github Pages. Pushing to the Github repository is equivalent to publishing the new version.

本文档使用Github Pages进行自动发布，对Github储存仓库的上传等同于新版本的发布。