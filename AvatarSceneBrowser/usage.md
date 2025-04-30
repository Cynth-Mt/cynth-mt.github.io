# 使用方法

## 编辑器使用

Avatar Scene Browser 提供了丰富的编辑器功能，帮助您在开发过程中管理和预览化身与场景。

### 打开浏览器窗口

1. 在 Unity 菜单中选择 `Tools > Avatar Scene Browser > Open Browser`
2. 或使用快捷键 `Ctrl+Shift+A` (Windows) / `Cmd+Shift+A` (Mac)

### 浏览和预览化身

1. 在浏览器左侧面板中，选择 `Avatars` 选项卡
2. 浏览可用的化身模型列表
3. 点击任意化身缩略图进行预览
4. 使用预览窗口中的控制按钮可以：
   - 旋转视角
   - 缩放预览
   - 切换动画状态
   - 调整灯光设置

### 场景管理

1. 切换到 `Scenes` 选项卡
2. 浏览可用场景列表
3. 点击场景缩略图预览场景
4. 使用右键菜单可以：
   - 在编辑器中打开场景
   - 将场景添加到构建设置
   - 复制场景

### 资源组织

1. 使用顶部的筛选器按类别或标签筛选资源
2. 使用搜索框查找特定资源
3. 通过拖放操作重新排列资源
4. 使用 `+` 按钮创建新的分类文件夹

## 运行时使用

以下是在运行时使用 Avatar Scene Browser 的基本方法：

### 初始化

```csharp
using CynLab.AvatarSceneBrowser;

public class MyGameManager : MonoBehaviour
{
    private AvatarSceneManager _manager;
    
    void Start()
    {
        // 初始化管理器
        _manager = new AvatarSceneManager();
        
        // 加载配置
        _manager.Initialize();
    }
}
```

### 加载和显示化身

```csharp
// 通过名称加载化身
_manager.LoadAvatar("MaleCharacter", OnAvatarLoaded);

// 回调函数
private void OnAvatarLoaded(AvatarInstance avatar)
{
    if (avatar != null)
    {
        // 成功加载化身
        avatar.gameObject.transform.position = new Vector3(0, 0, 0);
        
        // 播放动画
        avatar.PlayAnimation("Idle");
    }
    else
    {
        Debug.LogError("加载化身失败");
    }
}
```

### 切换场景

```csharp
// 加载新场景
_manager.LoadScene("ForestScene", LoadSceneMode.Single, OnSceneLoaded);

// 回调函数
private void OnSceneLoaded(bool success)
{
    if (success)
    {
        Debug.Log("场景加载成功");
        
        // 重新放置化身
        _manager.PlaceCurrentAvatarAtPoint(spawnPoint.position);
    }
}
```

### 保存和加载配置

```csharp
// 保存当前化身和场景组合
_manager.SaveCurrentSetup("我的配置");

// 稍后加载该配置
_manager.LoadSetup("我的配置");
```

## 高级使用

### 自定义化身属性

```csharp
// 获取当前化身
var avatar = _manager.CurrentAvatar;

// 修改属性
avatar.SetFloatProperty("Height", 1.8f);
avatar.SetColorProperty("SkinTone", new Color(0.9f, 0.8f, 0.7f));
avatar.SetTextureProperty("FaceTexture", myCustomTexture);

// 应用更改
avatar.ApplyProperties();
```

### 批量处理

```csharp
// 获取所有女性化身
var femaleAvatars = _manager.GetAvatarsByTag("female");

// 批量修改
foreach (var avatar in femaleAvatars)
{
    // 应用统一设置
    avatar.SetFloatProperty("HairLength", 0.7f);
}

// 批量导出
_manager.ExportAvatars(femaleAvatars, "Exports/FemaleCharacters");
```

## 提示与技巧

- **性能提示**：使用 `PreloadAvatars()` 方法预先加载常用化身，减少运行时延迟
- **内存管理**：不再使用的化身资源调用 `ReleaseAvatar()` 方法释放内存
- **动画过渡**：使用 `CrossFadeAnimation()` 方法实现平滑动画过渡
- **场景组合**：使用 `SceneSetup` 类保存和恢复完整的场景和化身组合 