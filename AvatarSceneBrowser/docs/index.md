# Avatar Scene Browser

<div class="grid cards" markdown>

-   :material-view-3d:{ .lg .middle } __现代化界面__

    ---

    简洁直观的用户界面，提供流畅的化身和场景管理体验

-   :material-lightning-bolt:{ .lg .middle } __高性能__

    ---

    优化的加载和渲染算法，确保大型项目的流畅运行

-   :material-puzzle:{ .lg .middle } __易于集成__

    ---

    无缝集成到现有Unity工作流程，最小化学习成本

-   :material-cog:{ .lg .middle } __高度可定制__

    ---

    丰富的API和配置选项，满足各种项目需求

</div>

!!! abstract "关于 Avatar Scene Browser"

    Avatar Scene Browser 是一个专为Unity开发的现代化工具插件，旨在简化虚拟化身和场景的管理、预览和使用流程。通过直观的界面和强大的功能，帮助开发者提高工作效率。

## :material-rocket-launch: 核心特性

### :material-account-multiple: 化身管理
- 支持多种格式：FBX、VRM、ReadyPlayerMe
- 智能分类和标签系统
- 批量导入和处理工具

### :material-earth: 场景浏览
- 实时场景预览
- 快速场景切换
- 场景状态保存和恢复

### :material-api: 运行时支持
- 完整的运行时API
- 异步加载系统
- 性能优化工具

## :material-play-circle: 快速开始

=== ":material-download: 安装"

    ```bash
    # 通过Unity Package Manager安装
    1. 打开Unity Package Manager
    2. 选择"Add package from git URL"
    3. 输入: https://github.com/cynth-mt/avatar-scene-browser.git
    4. 点击"Add"完成安装
    ```

=== ":material-cog: 配置"

    ```csharp
    using CynthMT.AvatarSceneBrowser;
    
    // 初始化管理器
    var manager = new AvatarSceneManager();
    
    // 设置资源路径
    manager.SetAvatarResourcePath("Assets/Resources/Avatars");
    manager.SetSceneResourcePath("Assets/Scenes");
    
    // 加载可用资源
    await manager.LoadAvailableAvatarsAsync();
    ```

=== ":material-rocket: 使用"

    ```csharp
    // 加载化身
    var avatar = await manager.LoadAvatarAsync("MyAvatar");
    
    // 切换场景
    await SceneBrowser.LoadSceneAsync("MyScene");
    
    // 预览模式
    manager.EnterPreviewMode();
    ```

---

## :material-check-circle: 兼容性

<div class="grid" markdown>

<div markdown>

### :material-unity: Unity版本
- :material-check: **2020.3 LTS**
- :material-check: **2021.3 LTS** 
- :material-check: **2022.3 LTS**
- :material-check: **2023.2+**

</div>

<div markdown>

### :material-palette: 渲染管线
- :material-check: **Built-in RP**
- :material-check: **URP** 
- :material-check: **HDRP**
- :material-check: **自定义管线**

</div>

</div>

---

## :material-navigation: 接下来

<div class="grid cards" markdown>

-   :material-book-open-page-variant:{ .lg .middle } __用户指南__

    ---

    从安装到配置的完整指南

    [:octicons-arrow-right-24: 开始使用](getting-started.md)

-   :material-puzzle:{ .lg .middle } __核心功能__

    ---

    了解化身管理和场景浏览功能

    [:octicons-arrow-right-24: 功能介绍](avatar-management.md)

-   :material-code-braces:{ .lg .middle } __开发者文档__

    ---

    API参考和代码示例

    [:octicons-arrow-right-24: API文档](api-reference.md)

-   :material-help-circle:{ .lg .middle } __获取帮助__

    ---

    常见问题和技术支持

    [:octicons-arrow-right-24: 常见问题](faq.md)

</div> 