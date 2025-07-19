# 单元测试

## 概述

Avatar Scene Browser插件包含完整的单元测试套件，确保代码质量和功能稳定性。本页面介绍如何运行测试和编写自定义测试。

## 测试框架

插件使用Unity Test Framework进行测试：

- **NUnit** - 单元测试框架
- **Unity Test Runner** - Unity集成测试工具
- **Moq** - 模拟对象框架

## 运行测试

### 通过Unity编辑器

1. 打开 **Window > General > Test Runner**
2. 选择 **PlayMode** 或 **EditMode** 标签
3. 点击 **Run All** 运行所有测试

### 命令行运行

```bash
Unity -batchmode -runTests -projectPath . -testResults results.xml
```

## 测试示例

### 化身加载测试

```csharp
using NUnit.Framework;
using UnityEngine;
using UnityEngine.TestTools;
using System.Collections;
using CynthMT.AvatarSceneBrowser;

public class AvatarLoaderTests
{
    [UnityTest]
    public IEnumerator LoadAvatar_ValidPath_ReturnsGameObject()
    {
        // Arrange
        string testAvatarPath = "Assets/TestAssets/TestAvatar.fbx";
        
        // Act
        var loadTask = AvatarSceneBrowser.LoadAvatarAsync(testAvatarPath);
        yield return new WaitUntil(() => loadTask.IsCompleted);
        
        // Assert
        Assert.IsNotNull(loadTask.Result);
        Assert.AreEqual("TestAvatar", loadTask.Result.name);
    }
    
    [Test]
    public void LoadAvatar_InvalidPath_ThrowsException()
    {
        // Arrange
        string invalidPath = "InvalidPath.fbx";
        
        // Act & Assert
        Assert.ThrowsAsync<System.IO.FileNotFoundException>(
            async () => await AvatarSceneBrowser.LoadAvatarAsync(invalidPath)
        );
    }
}
```

### 场景管理测试

```csharp
public class SceneBrowserTests
{
    [UnityTest]
    public IEnumerator LoadScene_ValidSceneName_LoadsSuccessfully()
    {
        // Arrange
        string testSceneName = "TestScene";
        
        // Act
        SceneBrowser.LoadScene(testSceneName);
        yield return new WaitForSeconds(1f);
        
        // Assert
        Assert.AreEqual(testSceneName, UnityEngine.SceneManagement.SceneManager.GetActiveScene().name);
    }
}
```

### 性能测试

```csharp
using Unity.PerformanceTesting;

public class PerformanceTests
{
    [Test, Performance]
    public void AvatarLoading_Performance_Test()
    {
        Measure.Method(() =>
        {
            // 测试化身加载性能
            var avatar = AvatarSceneBrowser.LoadAvatarSync("TestAvatar.fbx");
            Object.DestroyImmediate(avatar);
        })
        .WarmupCount(5)
        .MeasurementCount(10)
        .GC()
        .Run();
    }
}
```

## 模拟对象测试

### 使用Moq创建模拟对象

```csharp
using Moq;

public class AvatarManagerTests
{
    [Test]
    public void GetAvatar_ExistingId_ReturnsAvatar()
    {
        // Arrange
        var mockRepository = new Mock<IAvatarRepository>();
        var expectedAvatar = new AvatarData { Id = "test-id", Name = "Test Avatar" };
        mockRepository.Setup(r => r.GetById("test-id")).Returns(expectedAvatar);
        
        var manager = new AvatarManager(mockRepository.Object);
        
        // Act
        var result = manager.GetAvatar("test-id");
        
        // Assert
        Assert.AreEqual(expectedAvatar, result);
        mockRepository.Verify(r => r.GetById("test-id"), Times.Once);
    }
}
```

## 集成测试

### 端到端测试

```csharp
public class IntegrationTests
{
    [UnityTest]
    public IEnumerator CompleteWorkflow_LoadAvatarAndScene_WorksCorrectly()
    {
        // Arrange
        string avatarPath = "Assets/TestAssets/TestAvatar.fbx";
        string sceneName = "TestScene";
        
        // Act - 加载场景
        SceneBrowser.LoadScene(sceneName);
        yield return new WaitForSeconds(1f);
        
        // Act - 加载化身
        var loadTask = AvatarSceneBrowser.LoadAvatarAsync(avatarPath);
        yield return new WaitUntil(() => loadTask.IsCompleted);
        var avatar = loadTask.Result;
        
        // Assert
        Assert.IsNotNull(avatar);
        Assert.AreEqual(sceneName, UnityEngine.SceneManagement.SceneManager.GetActiveScene().name);
        Assert.IsTrue(avatar.activeInHierarchy);
    }
}
```

## 测试配置

### 测试程序集定义

创建 `Tests.asmdef` 文件：

```json
{
    "name": "AvatarSceneBrowser.Tests",
    "references": [
        "AvatarSceneBrowser",
        "UnityEngine.TestRunner",
        "UnityEditor.TestRunner"
    ],
    "includePlatforms": [],
    "excludePlatforms": [],
    "allowUnsafeCode": false,
    "overrideReferences": true,
    "precompiledReferences": [
        "nunit.framework.dll",
        "Moq.dll"
    ]
}
```

## 持续集成

### GitHub Actions测试配置

```yaml
- name: Run Unity Tests
  uses: game-ci/unity-test-runner@v2
  env:
    UNITY_LICENSE: ${{ secrets.UNITY_LICENSE }}
  with:
    projectPath: .
    testMode: all
    
- name: Upload Test Results
  uses: actions/upload-artifact@v2
  if: always()
  with:
    name: Test Results
    path: artifacts
```

## 最佳实践

1. **测试命名** - 使用描述性的测试名称
2. **AAA模式** - Arrange, Act, Assert
3. **独立测试** - 每个测试应该独立运行
4. **快速执行** - 保持测试运行速度
5. **覆盖率** - 维持高代码覆盖率 