# 示例代码

## 基础示例

### 简单的化身加载器

```csharp
using UnityEngine;
using CynthMT.AvatarSceneBrowser;

public class SimpleAvatarLoader : MonoBehaviour
{
    [SerializeField] private string avatarPath;
    
    async void Start()
    {
        // 初始化系统
        await AvatarSceneBrowser.InitializeAsync();
        
        // 加载化身
        var avatar = await AvatarSceneBrowser.LoadAvatarAsync(avatarPath);
        
        if (avatar != null)
        {
            Debug.Log($"成功加载化身: {avatar.name}");
        }
    }
}
```

### 场景切换器

```csharp
public class SceneSwitcher : MonoBehaviour
{
    [SerializeField] private string[] sceneNames;
    private int currentSceneIndex = 0;
    
    public void SwitchToNextScene()
    {
        currentSceneIndex = (currentSceneIndex + 1) % sceneNames.Length;
        SceneBrowser.LoadScene(sceneNames[currentSceneIndex]);
    }
}
```

## 高级示例

### 化身定制系统

```csharp
public class AvatarCustomizer : MonoBehaviour
{
    [System.Serializable]
    public class CustomizationOption
    {
        public string name;
        public GameObject[] variants;
    }
    
    [SerializeField] private CustomizationOption[] options;
    private GameObject currentAvatar;
    
    public void CustomizeAvatar(string optionName, int variantIndex)
    {
        var option = System.Array.Find(options, o => o.name == optionName);
        if (option != null && variantIndex < option.variants.Length)
        {
            // 应用自定义选项
            ApplyCustomization(option.variants[variantIndex]);
        }
    }
    
    private void ApplyCustomization(GameObject variant)
    {
        // 实现自定义逻辑
        if (currentAvatar != null)
        {
            // 替换或修改化身部件
            var targetSlot = currentAvatar.transform.Find("CustomizationSlot");
            if (targetSlot != null)
            {
                // 清除旧的自定义项
                for (int i = targetSlot.childCount - 1; i >= 0; i--)
                {
                    DestroyImmediate(targetSlot.GetChild(i).gameObject);
                }
                
                // 添加新的自定义项
                Instantiate(variant, targetSlot);
            }
        }
    }
}
```

### 动画控制器

```csharp
public class AvatarAnimationController : MonoBehaviour
{
    private Animator animator;
    private RuntimeAnimatorController defaultController;
    
    [SerializeField] private AnimationClip[] customAnimations;
    
    void Start()
    {
        animator = GetComponent<Animator>();
        defaultController = animator.runtimeAnimatorController;
    }
    
    public void PlayAnimation(string animationName)
    {
        var clip = System.Array.Find(customAnimations, a => a.name == animationName);
        if (clip != null)
        {
            animator.Play(animationName);
        }
    }
    
    public void SetAnimationSpeed(float speed)
    {
        animator.speed = speed;
    }
}
```

## 实用工具示例

### 化身信息显示器

```csharp
using UnityEngine.UI;

public class AvatarInfoDisplay : MonoBehaviour
{
    [SerializeField] private Text nameText;
    [SerializeField] private Text triangleCountText;
    [SerializeField] private Text materialCountText;
    
    public void DisplayAvatarInfo(GameObject avatar)
    {
        if (avatar == null) return;
        
        nameText.text = avatar.name;
        
        // 计算三角形数量
        int triangleCount = 0;
        var renderers = avatar.GetComponentsInChildren<Renderer>();
        foreach (var renderer in renderers)
        {
            var meshFilter = renderer.GetComponent<MeshFilter>();
            if (meshFilter != null && meshFilter.sharedMesh != null)
            {
                triangleCount += meshFilter.sharedMesh.triangles.Length / 3;
            }
        }
        triangleCountText.text = $"三角形: {triangleCount:N0}";
        
        // 计算材质数量
        int materialCount = 0;
        foreach (var renderer in renderers)
        {
            materialCount += renderer.materials.Length;
        }
        materialCountText.text = $"材质: {materialCount}";
    }
}
```

### 批量化身处理器

```csharp
public class BatchAvatarProcessor : MonoBehaviour
{
    [SerializeField] private string inputFolder;
    [SerializeField] private string outputFolder;
    
    [ContextMenu("Process All Avatars")]
    public async void ProcessAllAvatars()
    {
        var files = System.IO.Directory.GetFiles(inputFolder, "*.fbx");
        
        for (int i = 0; i < files.Length; i++)
        {
            var file = files[i];
            Debug.Log($"处理化身 {i + 1}/{files.Length}: {file}");
            
            try
            {
                var avatar = await AvatarSceneBrowser.LoadAvatarAsync(file);
                if (avatar != null)
                {
                    // 执行批处理操作
                    ProcessSingleAvatar(avatar);
                    
                    // 保存处理后的化身
                    var outputPath = System.IO.Path.Combine(outputFolder, 
                        System.IO.Path.GetFileName(file));
                    SaveProcessedAvatar(avatar, outputPath);
                }
            }
            catch (System.Exception ex)
            {
                Debug.LogError($"处理化身失败: {file}, 错误: {ex.Message}");
            }
        }
        
        Debug.Log("批量处理完成!");
    }
    
    private void ProcessSingleAvatar(GameObject avatar)
    {
        // 实现单个化身的处理逻辑
        // 例如：优化、标准化、添加组件等
    }
    
    private void SaveProcessedAvatar(GameObject avatar, string outputPath)
    {
        // 实现保存逻辑
        // 例如：保存为预制件、导出为文件等
    }
}
``` 