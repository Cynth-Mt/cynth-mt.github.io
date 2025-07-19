# 扩展开发

## 概述

Avatar Scene Browser插件提供了丰富的扩展接口，允许开发者根据自己的需求定制和扩展插件功能。本页面将介绍如何开发自定义扩展。

## 扩展架构

插件采用模块化架构，支持以下类型的扩展：

- **导入器扩展** - 支持新的化身格式
- **渲染器扩展** - 自定义渲染效果
- **UI扩展** - 添加自定义界面元素
- **工具扩展** - 集成外部工具

## 创建自定义导入器

```csharp
using CynthMT.AvatarSceneBrowser.Extensions;

[AvatarImporter("custom-format", "Custom Avatar Format")]
public class CustomAvatarImporter : IAvatarImporter
{
    public bool CanImport(string filePath)
    {
        return filePath.EndsWith(".custom");
    }
    
    public async Task<AvatarData> ImportAsync(string filePath)
    {
        // 实现自定义导入逻辑
        var avatarData = new AvatarData();
        // ... 处理文件
        return avatarData;
    }
}
```

## 开发UI扩展

```csharp
[CustomEditor(typeof(AvatarSceneBrowser))]
public class AvatarSceneBrowserEditor : Editor
{
    public override void OnInspectorGUI()
    {
        base.OnInspectorGUI();
        
        // 添加自定义UI元素
        if (GUILayout.Button("Custom Action"))
        {
            // 执行自定义操作
        }
    }
}
```

## 扩展注册

在插件初始化时注册您的扩展：

```csharp
[InitializeOnLoad]
public static class ExtensionRegistry
{
    static ExtensionRegistry()
    {
        AvatarSceneBrowser.RegisterExtension<CustomAvatarImporter>();
    }
}
``` 