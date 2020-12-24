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
> **TODO**： Note定义

> [!TIP]
>
> **TODO**： Tip定义

> [!WARNING]
>
> **TODO**： Warning定义

> [!ATTENTION]
>
> **TODO**: Attention定义

## Push and Release | 上传与发布
This document is automatically published using The Github Pages. Pushing to the Github repository is equivalent to publishing the new version.

本文档使用Github Pages进行自动发布，对Github储存仓库的上传等同于新版本的发布。