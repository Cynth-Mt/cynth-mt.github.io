# 运行时API

## 概述

Avatar Scene Browser插件提供了全面的运行时API，使您能够在游戏或应用程序运行期间动态管理化身和场景。本页面详细介绍了可用的运行时功能和使用方法。

## 初始化系统

在使用运行时API之前，您需要初始化Avatar Scene Browser系统：

```csharp
// 初始化Avatar Scene Browser系统
using CynthMT.AvatarSceneBrowser;

void Start()
{
    // 配置并初始化系统
    RuntimeManager.Initialize(new RuntimeConfig
    {
        preloadAvatars = true,
        asyncLoading = true,
        cacheSize = 10
    });
    
    Debug.Log("Avatar Scene Browser运行时系统已初始化");
}
```

## 化身管理API

### 加载化身

```csharp
// 通过ID加载化身
public async Task<GameObject> LoadAvatarAsync(string avatarId)
{
    // 异步加载化身
    GameObject avatar = await RuntimeManager.LoadAvatarAsync(avatarId);
    
    if (avatar != null)
    {
        // 配置化身
        RuntimeManager.SetupAvatar(avatar);
        return avatar;
    }
    
    Debug.LogError($"无法加载化身: {avatarId}");
    return null;
}
```

### 化身切换

```csharp
// 在角色上切换化身
public void SwitchAvatar(string characterId, string newAvatarId)
{
    // 获取角色引用
    Character character = RuntimeManager.GetCharacter(characterId);
    
    if (character != null)
    {
        // 更换化身
        RuntimeManager.SwitchAvatar(character, newAvatarId, (success) => {
            if (success)
                Debug.Log("化身切换成功");
            else
                Debug.LogError("化身切换失败");
        });
    }
}
```

## 场景管理API

### 场景加载

```csharp
// 加载场景并显示进度
public async void LoadSceneWithProgress(string sceneId, Action<float> progressCallback)
{
    // 开始异步加载
    SceneLoadingOperation operation = RuntimeManager.LoadSceneAsync(sceneId);
    
    // 设置进度回调
    operation.OnProgressChanged += (progress) => {
        progressCallback?.Invoke(progress);
    };
    
    // 等待完成
    await operation.Task;
    
    Debug.Log($"场景 {sceneId} 加载完成");
}
```

### 场景叠加

```csharp
// 叠加加载场景
public void AddSceneLayer(string sceneId)
{
    RuntimeManager.LoadSceneAdditive(sceneId, (success) => {
        if (success)
            Debug.Log($"叠加场景 {sceneId} 加载成功");
    });
}
```

## 事件系统

Avatar Scene Browser提供了丰富的事件回调系统，方便您响应各种运行时事件：

```csharp
void SubscribeToEvents()
{
    // 订阅化身加载事件
    RuntimeManager.OnAvatarLoaded += HandleAvatarLoaded;
    
    // 订阅场景切换事件
    RuntimeManager.OnSceneChanged += HandleSceneChanged;
    
    // 订阅错误事件
    RuntimeManager.OnError += HandleError;
}

void HandleAvatarLoaded(AvatarLoadedEventArgs args)
{
    Debug.Log($"化身 {args.AvatarId} 已加载，用时: {args.LoadTime}秒");
}

void HandleSceneChanged(SceneChangedEventArgs args)
{
    Debug.Log($"从场景 {args.PreviousSceneId} 切换到 {args.CurrentSceneId}");
}

void HandleError(ErrorEventArgs args)
{
    Debug.LogError($"错误: {args.Message}, 类型: {args.ErrorType}");
}
```

## 性能优化

运行时API提供了多种性能优化选项：

### 缓存管理

```csharp
// 配置化身缓存
RuntimeManager.ConfigureCache(new CacheConfig
{
    maxAvatars = 5,
    maxScenes = 3,
    preloadCommon = true
});

// 预加载常用化身
RuntimeManager.PreloadAvatars(new[] { "avatar_001", "avatar_002" });
```

### 资源释放

```csharp
// 释放不需要的资源
public void ReleaseUnusedResources()
{
    // 释放未使用的化身
    RuntimeManager.ReleaseUnusedAvatars();
    
    // 卸载不活跃的场景
    RuntimeManager.UnloadInactiveScenes();
    
    // 强制垃圾回收
    System.GC.Collect();
}
```

## 示例用例

以下是一个完整的运行时管理器示例：

```csharp
using UnityEngine;
using System.Collections.Generic;
using CynthMT.AvatarSceneBrowser;

public class AvatarSceneManager : MonoBehaviour
{
    [SerializeField] private string defaultAvatarId;
    [SerializeField] private string defaultSceneId;
    
    private void Start()
    {
        // 初始化系统
        InitializeSystem();
        
        // 订阅事件
        SubscribeEvents();
        
        // 加载默认场景和化身
        LoadDefaultContent();
    }
    
    private void InitializeSystem()
    {
        RuntimeManager.Initialize(new RuntimeConfig
        {
            preloadAvatars = true,
            asyncLoading = true,
            logLevel = LogLevel.Verbose
        });
    }
    
    private void SubscribeEvents()
    {
        RuntimeManager.OnAvatarLoaded += (args) => Debug.Log("化身已加载");
        RuntimeManager.OnSceneChanged += (args) => Debug.Log("场景已切换");
    }
    
    private async void LoadDefaultContent()
    {
        // 加载默认场景
        await RuntimeManager.LoadSceneAsync(defaultSceneId).Task;
        
        // 加载默认化身
        GameObject avatar = await RuntimeManager.LoadAvatarAsync(defaultAvatarId);
        
        if (avatar != null)
        {
            // 放置化身在场景中
            avatar.transform.position = Vector3.zero;
        }
    }
    
    private void OnDestroy()
    {
        // 清理资源
        RuntimeManager.Shutdown();
    }
}
``` 