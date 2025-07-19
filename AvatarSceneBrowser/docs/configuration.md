# 基本配置

## 配置概述

Avatar Scene Browser 提供了多种配置选项，使您能够根据项目需求调整插件行为。本文档介绍了主要的配置项及其设置方法。

## 全局设置

### 通过编辑器界面配置

1. 打开 Unity 编辑器
2. 选择 `Tools > Avatar Scene Browser > Settings`
3. 在设置面板中调整以下选项：
   - **资源路径**：设置化身模型和场景资源的默认路径
   - **缓存大小**：调整预览缓存的大小（以MB为单位）
   - **默认预览背景**：选择预览窗口的默认背景
   - **启用高级功能**：打开/关闭高级功能集

### 通过代码配置

您也可以通过代码动态设置配置：

```csharp
// 获取配置实例
var config = AvatarSceneBrowserConfig.Instance;

// 设置资源路径
config.SetAvatarResourcePath("Assets/Resources/CustomAvatars");
config.SetSceneResourcePath("Assets/Resources/CustomScenes");

// 调整缓存大小
config.SetCacheSize(512); // 以MB为单位

// 保存配置
config.SaveConfig();
```

## 项目特定配置

### 化身配置文件

在项目根目录创建 `avatar-config.json` 文件可以定义特定的化身配置：

```json
{
  "defaultAvatars": [
    "MaleBase",
    "FemaleBase"
  ],
  "avatarCategories": [
    {
      "name": "人类角色",
      "tag": "human"
    },
    {
      "name": "动物角色",
      "tag": "animal"
    }
  ],
  "previewSettings": {
    "camera": {
      "position": [0, 1.7, 2.5],
      "rotation": [0, 180, 0]
    },
    "lighting": "studio"
  }
}
```

### 场景配置文件

同样，您可以创建 `scene-config.json` 文件来配置场景相关设置：

```json
{
  "defaultScenes": [
    "EmptyStudio",
    "OutdoorNature"
  ],
  "sceneCategories": [
    {
      "name": "室内场景",
      "tag": "indoor"
    },
    {
      "name": "室外场景",
      "tag": "outdoor"
    }
  ]
}
```

## 高级配置

### 性能优化设置

可在高级设置中调整以下性能参数：

- **LOD级别**：设置模型的细节级别
- **最大同时加载数**：限制同时加载的资源数量
- **预加载策略**：配置预加载行为

### 自定义渲染设置

针对不同渲染管线的特定设置：

- **URP设置**：调整URP专用参数
- **HDRP设置**：配置HDRP特定功能
- **Built-in设置**：传统渲染管线参数

## 配置文件位置

所有配置文件默认保存在以下位置：

- 编辑器设置: `ProjectSettings/AvatarSceneBrowser/`
- 运行时设置: `Assets/Resources/AvatarSceneBrowser/Config/`

您可以通过备份这些文件在不同项目之间共享配置。 