#  编写规范
本部分包括了对文档编写规范的约束。

## 文件结构

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
>不要修改文件结构与`index.html`，这将会导致发布页面异常

## 提示与警告

对提示与警告的使用做出如下规定，请在编写文档时注意。

> [!NOTE]
> 
> 该级别用于提供**文档内容的说明**或**外部链接的引用**
> 
> *举例： 简短说明CARAL额外下载的资产包括什么内容*

> [!TIP]
> 
> 该级别用于提供**最佳实践**或**最佳实践的引用**
>
> *举例： 最佳的CARAL版本管理方式*

> [!WARNING]
> 
> 该级别用于警示可能**引发应用程序使用问题**的操作
> 
> *举例： 在zsh中引用了setup.bash*

> [!ATTENTION]
> 
> 该级别用于警示一定会**引发严重问题**或**系统环境错误**的操作
> 
> *举例： 对操作系统Python版本的操作*

### 使用警示

在使用提示框时，标点符号（不论中英文）必须后跟空格，否则会在渲染时丢失整个提示框。

## 上传与发布

本文档使用Github Pages进行自动发布，对Github储存仓库的上传等同于新版本的发布。