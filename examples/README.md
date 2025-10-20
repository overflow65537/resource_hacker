# 使用示例

本目录包含了各种使用场景的示例工作流文件。

## 📁 文件说明

### `basic-usage.yml`
最简单的使用示例，演示如何替换单个应用程序的图标。

**适用场景**：
- 快速替换图标
- 简单的 CI/CD 流程

### `advanced-usage.yml`
高级用法示例，包含：
- 多个应用程序的图标替换
- 自定义资源名称
- 工作流输入参数
- 批量处理

**适用场景**：
- 处理多个可执行文件
- 需要灵活配置的场景
- 动态图标选择

### `dotnet-build.yml`
.NET 应用程序完整构建和图标替换流程。

**适用场景**：
- .NET Framework / .NET Core 项目
- 完整的构建、发布、自定义流程
- 创建发布版本

### `python-app.yml`
Python 应用程序使用 PyInstaller 打包并替换图标。

**适用场景**：
- Python GUI 应用
- PyInstaller 打包的项目
- 需要自定义图标的 Python 可执行文件

## 🚀 如何使用这些示例

1. **选择合适的示例**：根据你的项目类型选择对应的示例文件

2. **复制到你的仓库**：
   ```bash
   # 创建工作流目录
   mkdir -p .github/workflows
   
   # 复制示例文件
   cp examples/basic-usage.yml .github/workflows/
   ```

3. **修改配置**：
   - 更新文件路径
   - 调整触发条件
   - 修改参数值

4. **准备资源文件**：
   - 确保 `.ico` 文件存在
   - 确保可执行文件路径正确

5. **提交并运行**：
   ```bash
   git add .github/workflows/
   git commit -m "Add icon replacement workflow"
   git push
   ```

## 💡 提示

### 创建 .ico 文件
如果你需要创建 `.ico` 图标文件，可以使用：
- [IcoConverter](https://www.icoconverter.com/) - 在线转换工具
- [GIMP](https://www.gimp.org/) - 开源图像编辑器
- [ImageMagick](https://imagemagick.org/) - 命令行工具

### 图标尺寸建议
推荐包含以下尺寸：
- 16x16
- 32x32
- 48x48
- 256x256

### 常见问题

**Q: 如何验证图标是否替换成功？**
```yaml
- name: Verify icon
  shell: powershell
  run: |
    if (Test-Path "app.exe") {
      Write-Host "✅ File exists and has been modified"
    }
```

**Q: 能否同时替换多个资源？**

可以多次调用 Action：
```yaml
- name: Replace main icon
  uses: overflow65537/resource_hacker@v1
  with:
    exe-path: 'app.exe'
    icon-path: 'icon1.ico'
    resource-name: 'MAINICON'

- name: Replace alternate icon
  uses: overflow65537/resource_hacker@v1
  with:
    exe-path: 'app.exe'
    icon-path: 'icon2.ico'
    resource-name: 'ALTICON'
```

**Q: 如何在本地测试？**

可以使用 [act](https://github.com/nektos/act) 在本地运行 GitHub Actions：
```bash
act -j replace-icon
```

## 📚 更多资源

- [GitHub Actions 文档](https://docs.github.com/en/actions)
- [Resource Hacker 文档](https://angusj.com/resourcehacker/)
- [项目主页](https://github.com/overflow65537/resource_hacker)
