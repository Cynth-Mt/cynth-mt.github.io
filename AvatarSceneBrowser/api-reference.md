# API参考

## 核心类

### AvatarSceneManager

主要管理类，负责所有化身和场景操作。

#### 公共属性

| 属性名 | 类型 | 描述 |
|--------|------|------|
| CurrentAvatar | AvatarInstance | 当前活动的化身实例 |
| AvailableAvatars | List<AvatarInfo> | 所有可用的化身信息 |
| AvailableScenes | List<SceneInfo> | 所有可用的场景信息 |
| IsInitialized | bool | 管理器是否已初始化 |

#### 公共方法

| 方法名 | 参数 | 返回值 | 描述 |
|--------|------|--------|------|
| Initialize | - | void | 初始化管理器和配置 |
| LoadAvatar | string name, Action<AvatarInstance> callback | void | 异步加载指定名称的化身 |
| LoadAvatarSync | string name | AvatarInstance | 同步加载指定名称的化身 |
| ReleaseAvatar | AvatarInstance avatar | void | 释放化身实例占用的资源 |
| LoadScene | string name, LoadSceneMode mode, Action<bool> callback | void | 加载指定名称的场景 |
| PreloadAvatars | List<string> avatarNames | void | 预加载多个化身资源 |
| GetAvatarsByTag | string tag | List<AvatarInfo> | 获取带有指定标签的所有化身 |
| SaveCurrentSetup | string name | bool | 保存当前化身和场景设置 |
| LoadSetup | string name | bool | 加载已保存的设置组合 |

### AvatarInstance

代表单个化身实例的类。

#### 公共属性

| 属性名 | 类型 | 描述 |
|--------|------|------|
| GameObject | GameObject | 化身的Unity游戏对象 |
| Info | AvatarInfo | 化身的静态信息 |
| IsActive | bool | 化身是否处于活动状态 |

#### 公共方法

| 方法名 | 参数 | 返回值 | 描述 |
|--------|------|--------|------|
| PlayAnimation | string animName | bool | 播放指定名称的动画 |
| CrossFadeAnimation | string animName, float fadeTime | bool | 平滑过渡到指定动画 |
| SetFloatProperty | string propName, float value | void | 设置浮点类型属性 |
| SetColorProperty | string propName, Color value | void | 设置颜色类型属性 |
| SetTextureProperty | string propName, Texture value | void | 设置纹理类型属性 |
| ApplyProperties | - | void | 应用所有属性更改 |
| SetVisibility | bool visible | void | 设置化身可见性 |

### SceneInfo

场景信息类。

#### 公共属性

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Name | string | 场景名称 |
| Path | string | 场景文件路径 |
| PreviewTexture | Texture2D | 场景预览图 |
| Tags | List<string> | 场景标签列表 |
| Category | string | 场景类别 |

## 实用工具类

### AvatarUtility

提供化身相关的实用功能。

#### 静态方法

| 方法名 | 参数 | 返回值 | 描述 |
|--------|------|--------|------|
| GeneratePreview | GameObject avatarObject, Vector2 size | Texture2D | 生成化身的预览图 |
| OptimizeAvatar | GameObject avatar, OptimizationLevel level | void | 优化化身模型 |
| ExportAvatarToPrefab | AvatarInstance avatar, string path | bool | 将化身导出为预制体 |

### SceneUtility

提供场景相关的实用功能。

#### 静态方法

| 方法名 | 参数 | 返回值 | 描述 |
|--------|------|--------|------|
| GenerateScenePreview | string scenePath, Vector2 size | Texture2D | 生成场景的预览图 |
| GetSceneLighting | string sceneName | LightingInfo | 获取场景的光照信息 |
| GetSceneObjects | string sceneName, string tag | List<GameObject> | 获取场景中带有特定标签的所有对象 |

## 配置类

### AvatarSceneBrowserConfig

管理插件配置的静态类。

#### 静态属性

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Instance | AvatarSceneBrowserConfig | 配置单例实例 |

#### 公共方法

| 方法名 | 参数 | 返回值 | 描述 |
|--------|------|--------|------|
| SetAvatarResourcePath | string path | void | 设置化身资源路径 |
| SetSceneResourcePath | string path | void | 设置场景资源路径 |
| SetCacheSize | int sizeInMB | void | 设置缓存大小 |
| SaveConfig | - | void | 保存当前配置 |
| LoadConfig | - | void | 加载保存的配置 |
| ResetToDefaults | - | void | 重置为默认配置 |

## 枚举类型

### OptimizationLevel

定义化身优化的级别。

| 值 | 描述 |
|-----|------|
| None | 不进行优化 |
| Low | 轻度优化，适合高性能设备 |
| Medium | 中度优化，适合中等性能设备 |
| High | 高度优化，适合低性能设备 |

### AvatarState

定义化身的状态。

| 值 | 描述 |
|-----|------|
| Loading | 化身正在加载中 |
| Ready | 化身已加载并准备好 |
| Error | 化身加载出错 |
| Released | 化身已被释放 |

## 事件

### AvatarSceneManager事件

| 事件名 | 事件处理器类型 | 描述 |
|--------|--------------|------|
| OnAvatarLoaded | Action<AvatarInstance> | 化身加载完成时触发 |
| OnSceneLoaded | Action<bool> | 场景加载完成时触发 |
| OnConfigChanged | Action | 配置更改时触发 |
| OnManagerInitialized | Action | 管理器初始化完成时触发 |

## 异常类型

| 异常名 | 继承自 | 描述 |
|--------|------|------|
| AvatarNotFoundException | Exception | 找不到指定化身时抛出 |
| SceneNotFoundException | Exception | 找不到指定场景时抛出 |
| ConfigurationException | Exception | 配置错误时抛出 |
| ResourceLoadException | Exception | 资源加载失败时抛出 | 