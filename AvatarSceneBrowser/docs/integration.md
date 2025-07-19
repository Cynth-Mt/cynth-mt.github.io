# 集成第三方资源

## 概述

Avatar Scene Browser插件支持与多种第三方工具和资源库的集成，扩展其功能和兼容性。

## VRM支持

### VRM 1.0集成

```csharp
using UniVRM10;

public class VRMIntegration
{
    public async Task<GameObject> LoadVRM(string filePath)
    {
        var instance = await Vrm10.LoadPathAsync(filePath);
        return instance.gameObject;
    }
}
```

### VRM表情系统

- 支持VRM表情预设
- 自定义表情混合
- 实时表情控制

## Ready Player Me

### RPM化身集成

```csharp
public class RPMIntegration
{
    public async Task<GameObject> LoadRPMAvatar(string avatarUrl)
    {
        var loader = new AvatarLoader();
        return await loader.LoadAvatar(avatarUrl);
    }
}
```

## Mixamo动画

### 动画导入

- 支持Mixamo动画库
- 自动重定向到化身骨骼
- 动画混合和过渡

## 第三方资源商店

### 兼容的资源包

- **Final IK** - 高级IK系统集成
- **Puppet Master** - 物理动画系统
- **Salsa 3D** - 嘴唇同步
- **Crazy Minnow Studio SALSA** - 面部动画

### 集成示例

```csharp
// Final IK集成
public void SetupFinalIK(GameObject avatar)
{
    var ik = avatar.AddComponent<FullBodyBipedIK>();
    ik.solver.SetToReferences(avatar.GetComponent<Animator>());
}
```

## 自定义集成

### 创建集成适配器

```csharp
public abstract class ThirdPartyIntegration
{
    public abstract string Name { get; }
    public abstract bool IsAvailable { get; }
    public abstract void Initialize();
    public abstract void ProcessAvatar(GameObject avatar);
}
``` 