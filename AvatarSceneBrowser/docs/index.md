# Avatar Scene Browser 插件文档

<div class="grid cards" markdown>

-   :fontawesome-solid-rocket:{ .lg .middle } __快速开始__

    ---

    几分钟内即可安装并开始使用Avatar Scene Browser

    [:octicons-arrow-right-24: 开始使用](getting-started.md)

-   :fontawesome-solid-cubes:{ .lg .middle } __功能丰富__

    ---

    支持多种化身格式，提供完整的场景管理解决方案

    [:octicons-arrow-right-24: 功能模块](avatar-management.md)

-   :fontawesome-solid-code:{ .lg .middle } __开发友好__

    ---

    提供完整的API文档和示例代码

    [:octicons-arrow-right-24: API参考](api-reference.md)

-   :fontawesome-solid-heart:{ .lg .middle } __开源免费__

    ---

    MIT许可证，完全免费使用和修改

    [:octicons-arrow-right-24: GitHub](https://github.com/cynth-mt/cynth-mt.github.io)

</div>

!!! tip "插件简介"
    Avatar Scene Browser是一个专为Unity开发的工具插件，旨在简化虚拟化身和场景的管理、预览和使用流程。无论您是独立开发者还是大型团队，都能从中受益。

## 主要功能

- **化身模型预览与管理** - 支持多种格式的化身导入和组织
- **场景快速切换与编辑** - 高效的场景管理和预览系统
- **自定义化身属性配置** - 灵活的化身参数调整
- **批量处理工具集** - 提高工作效率的批处理功能
- **实时预览与调试** - 所见即所得的编辑体验

## 快速开始

=== "安装插件"

    1. 打开Unity Package Manager
    2. 选择"Add package from git URL"
    3. 输入插件的Git URL
    4. 点击"Add"完成安装

=== "基本配置"

    ```csharp
    // 初始化Avatar Scene Browser管理器
    AvatarSceneManager manager = new AvatarSceneManager();
    
    // 配置化身资源路径
    manager.SetAvatarResourcePath("Assets/Resources/Avatars");
    
    // 加载当前场景中所有可用的化身
    manager.LoadAvailableAvatars();
    ```

=== "快速使用"

    ```csharp
    // 预览指定的化身模型
    manager.PreviewAvatar("AvatarName");
    
    // 切换到新场景
    SceneBrowser.LoadScene("NewSceneName");
    ```

## 适用版本

| Unity版本 | 支持状态 |
|-----------|----------|
| 2020.3 LTS | ✅ 完全支持 |
| 2021.3 LTS | ✅ 完全支持 |
| 2022.3 LTS | ✅ 完全支持 |
| 2023.1+ | ✅ 完全支持 |

## 渲染管线支持

- Built-in Render Pipeline
- Universal Render Pipeline (URP)
- High Definition Render Pipeline (HDRP)

## 下一步

- [开始使用](getting-started.md) - 详细的安装和配置指南
- [功能模块](avatar-management.md) - 了解插件的核心功能
- [API参考](api-reference.md) - 完整的API文档 