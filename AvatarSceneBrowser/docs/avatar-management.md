# 化身管理

## 概述

Avatar Scene Browser插件提供了全面的化身管理功能，使您能够轻松导入、组织和操作各种虚拟化身模型。本页面将详细介绍相关功能和使用方法。

## 化身导入

### 支持的格式

插件支持以下化身模型格式：
- FBX格式
- VRM格式（1.0和0.x）
- Unity自定义Avatar格式
- ReadyPlayerMe格式

### 导入步骤

1. 在Unity编辑器中，选择菜单 **Avatar Scene Browser > Import Avatar**
2. 在弹出的窗口中选择您要导入的模型文件
3. 配置导入选项（如是否带材质、动画等）
4. 点击"导入"按钮完成操作

## 化身组织

### 化身库

插件包含一个化身库系统，使您可以：
- 按类别分组管理化身
- 为化身添加标签和描述
- 搜索和筛选化身

### 化身分组

您可以创建自定义分组来组织您的化身：
1. 在化身浏览器中点击"新建分组"按钮
2. 输入分组名称
3. 将化身拖拽到分组中

## 化身预览

### 3D预览

- 360度旋转查看
- 测试骨骼和动画
- 调整相机参数

### 快照功能

- 捕捉化身的2D缩略图
- 自定义背景和姿势
- 批量生成预览图

## 化身编辑

### 基本属性

- 重命名和描述
- 调整缩放和位置
- 设置骨骼映射

### 高级自定义

- 材质编辑
- 骨骼权重修改
- 表情系统设置

## 示例代码

```csharp
// 加载化身示例
public void LoadAvatar(string avatarId)
{
    // 从化身库获取化身数据
    AvatarData data = AvatarSceneBrowser.GetAvatarById(avatarId);
    
    // 实例化化身
    GameObject avatarInstance = AvatarSceneBrowser.InstantiateAvatar(data);
    
    // 配置化身
    AvatarSetup setup = avatarInstance.GetComponent<AvatarSetup>();
    setup.Initialize();
    
    Debug.Log($"Avatar {data.name} loaded successfully!");
}
``` 