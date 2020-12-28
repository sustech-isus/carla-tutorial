# Edit Rules ｜ 编写规范
This section includes constraints on the documentation specification.

本部分包括了对文档编写规范的约束。

## Structure | 文件结构

```
carla-tutorial
├── demo                // => Demo codes | 演示用代码
├── docs                // => Documents | 文档相关文件
│   ├── README.md       // => Main page ｜ 文档主页
|   ├── intro.md        // => Introduction | 项目概述
|   ├── _sidebar.md     // => Sidebar | 侧边栏导航
|   ├── resources.md    // => Ralated Resources | 相关资源
|   ├── rules.md        // => Writing Rules | 文档规范
│   └── quick_start    
│       └── README.md  
└── images              // => Images storage | 图片储存
```

> [!ATTENTION]
>
> Do not modify the file structure or `index.html`, which will result in a publish page exception.
>
>不要修改文件结构与`index.html`，这将会导致发布页面异常

## Notice and Warning | 提示与警告
The following rules apply to the use of notice and warnings. Please pay attention to them when writing documents.

对提示与警告的使用做出如下规定，请在编写文档时注意。

> [!NOTE]
> 
> 该级别用于提供**文档内容的说明**或**外部链接的引用**
> 
> *举例：简短说明CARAL额外下载的资产包括什么内容*
<!-- > **TODO**： Note定义 -->


> [!TIP]
> 
> 该级别用于提供**最佳实践**或**最佳实践的引用**
>
> *举例：最佳的CARAL版本管理方式*
> 
<!-- > **TODO**： Tip定义 -->

> [!WARNING]
> 
> 该级别用于警示可能**引发应用程序使用问题**的操作
> 
> *举例：在zsh中引用了setup.bash*
<!-- > **TODO**： Warning定义 -->

> [!ATTENTION]
> 
> 该级别用于警示一定会**引发严重问题**或**系统环境错误**的操作
> 
> *举例：对操作系统Python版本的操作*

## Push and Release | 上传与发布
This document is automatically published using The Github Pages. Pushing to the Github repository is equivalent to publishing the new version.

本文档使用Github Pages进行自动发布，对Github储存仓库的上传等同于新版本的发布。