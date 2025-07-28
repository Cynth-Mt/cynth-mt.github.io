# 开始使用

## 概述

本文档将引导您完成 Avatar Scene Browser 插件的初始设置和基本使用流程。通过几个简单的步骤，您就可以在Unity项目中集成并使用这个功能强大的化身场景管理工具。

## 前提条件

在开始使用 Avatar Scene Browser 之前，请确保您的开发环境满足以下条件：

- Unity 2020.3 LTS 或更高版本
- 基本了解Unity编辑器操作
- 项目中已导入需要管理的化身模型和场景资源

## 安装步骤

详细的安装步骤请参考[安装指南](installation.md)。简要步骤如下：

1. 通过Unity Package Manager导入插件
2. 设置项目配置
3. 初始化插件管理器

## 快速入门示例

以下是一个简单的示例，展示如何快速设置和使用该插件：

```csharp
// 初始化Avatar Scene Browser管理器
AvatarSceneManager manager = new AvatarSceneManager();

// 配置化身资源路径
manager.SetAvatarResourcePath("Assets/Resources/Avatars");

// 加载当前场景中所有可用的化身
manager.LoadAvailableAvatars();

// 预览指定的化身模型
manager.PreviewAvatar("AvatarName");
```

## 下一步

完成基本设置后，您可以：

- 阅读[基本配置](configuration.md)了解更多配置选项
- 查看[使用方法](usage.md)获取详细的功能使用说明
- 参考[API文档](runtime-api.md)进行高级开发 