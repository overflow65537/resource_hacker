# 快速开始指南

欢迎使用 Resource Hacker Icon Replacer Action！ 🎉

## ⚡ 5 分钟快速上手

### 第 1 步：准备文件

确保您有：
- ✅ Windows 可执行文件（`.exe`）
- ✅ 图标文件（`.ico` 格式）

### 第 2 步：创建工作流

在您的仓库中创建 `.github/workflows/replace-icon.yml`：

```yaml
name: Replace Icon

on:
  push:
    branches: [ main ]

jobs:
  customize:
    runs-on: windows-latest
    
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Replace Icon
        uses: overflow65537/resource_hacker@v1
        with:
          exe-path: 'app.exe'      # 您的 exe 文件路径
          icon-path: 'icon.ico'    # 您的 ico 文件路径
```

### 第 3 步：提交并运行

```bash
git add .github/workflows/replace-icon.yml
git commit -m "Add icon replacement workflow"
git push
```

就这么简单！ 🎊

## 📝 常见用例

### 用例 1: 构建后替换图标

```yaml
- name: Build app
  run: dotnet build -c Release

- name: Replace icon
  uses: overflow65537/resource_hacker@v1
  with:
    exe-path: 'bin/Release/MyApp.exe'
    icon-path: 'assets/icon.ico'
```

### 用例 2: 保存为新文件

```yaml
- name: Replace icon (create new file)
  uses: overflow65537/resource_hacker@v1
  with:
    exe-path: 'original.exe'
    icon-path: 'new-icon.ico'
    output-path: 'customized.exe'  # 不覆盖原文件
```

### 用例 3: 使用输出路径

```yaml
- name: Replace icon
  id: replace
  uses: overflow65537/resource_hacker@v1
  with:
    exe-path: 'app.exe'
    icon-path: 'icon.ico'

- name: Show result
  run: echo "Output: ${{ steps.replace.outputs.output-file }}"
```

## 🎯 输入参数快速参考

| 参数 | 必需 | 说明 | 示例 |
|------|------|------|------|
| `exe-path` | ✅ | 可执行文件路径 | `'app.exe'` |
| `icon-path` | ✅ | 图标文件路径 | `'icon.ico'` |
| `output-path` | ❌ | 输出路径（可选） | `'out.exe'` |

## ❓ 常见问题

### Q: 支持哪些文件格式？
- 可执行文件：`.exe`, `.dll`, `.scr` 等 Windows PE 文件
- 图标文件：`.ico` 格式（必须）

### Q: 需要安装 Resource Hacker 吗？
不需要！Action 会自动下载。

### Q: 可以在 Linux/Mac 上运行吗？
不行，必须使用 `runs-on: windows-latest`

### Q: 如何创建 .ico 文件？
使用在线工具：https://www.icoconverter.com/

## 🔗 下一步

- 📚 查看 [完整文档](README.md)
- 💡 浏览 [示例](examples/)
- 🐛 [报告问题](https://github.com/overflow65537/resource_hacker/issues)
- 🤝 [贡献代码](CONTRIBUTING.md)

## 💬 需要帮助？

如果遇到问题：
1. 查看 [故障排除](README.md#故障排除)
2. 检查 [示例](examples/)
3. [创建 Issue](https://github.com/overflow65537/resource_hacker/issues/new)

祝您使用愉快！ 🚀
