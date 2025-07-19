# 安装指南

## 安装方式

Avatar Scene Browser 插件提供多种安装方式，您可以根据自己的需求选择最合适的方式：

### 方式一：通过 Unity Package Manager

1. 打开 Unity 项目
2. 选择菜单 `Window > Package Manager`
3. 点击左上角的 `+` 按钮
4. 选择 `Add package from git URL...`
5. 输入: `https://github.com/cynlab/AvatarSceneBrowser.git`
6. 点击 `Add` 按钮

### 方式二：导入 Unity Package

1. 从[发布页面](https://github.com/cynlab/AvatarSceneBrowser/releases)下载最新的 `.unitypackage` 文件
2. 在 Unity 编辑器中，选择 `Assets > Import Package > Custom Package...`
3. 选择下载的 `.unitypackage` 文件
4. 在导入窗口中确认所有文件都被选中，然后点击 `Import`

### 方式三：手动安装

1. 下载或克隆仓库: `git clone https://github.com/cynlab/AvatarSceneBrowser.git`
2. 将 `AvatarSceneBrowser/Assets/Plugins/AvatarSceneBrowser` 文件夹复制到您的项目的 `Assets/Plugins` 目录下

## 验证安装

安装完成后，您可以通过以下步骤验证安装是否成功：

1. 在 Unity 菜单中，应该出现 `Tools > Avatar Scene Browser` 选项
2. 点击该选项，应该能打开 Avatar Scene Browser 窗口
3. 检查 Project 面板中是否存在 `Plugins/AvatarSceneBrowser` 文件夹

## 配置依赖项

Avatar Scene Browser 依赖于以下插件，请确保它们已正确安装：

- Unity Addressables (版本 1.18.0 或更高)
- Unity UI (内置包)

如果缺少这些依赖项，插件将自动提示您安装。

## 故障排除

如果在安装过程中遇到问题，请尝试以下解决方案：

- 确保您的 Unity 版本兼容 (Unity 2020.3 LTS 或更高版本)
- 检查控制台是否有错误消息
- 尝试重启 Unity 编辑器
- 确保您有足够的权限来导入和安装包

如果问题仍然存在，请[提交问题](https://github.com/cynlab/AvatarSceneBrowser/issues)并提供详细的错误信息。 