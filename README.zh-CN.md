# Resource Hacker Icon Replacer Action

**[English](README.md) | 简体中文**

[![GitHub release](https://img.shields.io/github/v/release/overflow65537/resource_hacker)](https://github.com/overflow65537/resource_hacker/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

🎨 一个 GitHub Action，用于自动替换 Windows 应用程序的图标。该 Action 会自动下载并使用 [Resource Hacker™](https://angusj.com/resourcehacker/)。

## ✨ 特性

- 🚀 **自动化**：无需手动安装 Resource Hacker，Action 会自动下载
- 🎯 **简单易用**：只需提供 exe 文件和 ico 图标即可
- 🔧 **灵活配置**：支持自定义资源名称、类型和语言
- 📦 **轻量级**：不包含任何第三方可执行文件
- ✅ **可靠**：包含完整的错误检查和日志输出

## 📋 前置要求

- Windows 运行环境（使用 `runs-on: windows-latest`）
- 有效的 `.ico` 图标文件
- 目标 Windows 可执行文件（`.exe`）

## 🚀 使用方法

### 基础用法

```yaml
name: Replace App Icon

on:
  push:
    branches: [ main ]

jobs:
  replace-icon:
    runs-on: windows-latest
    
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      
      - name: Replace icon
        uses: overflow65537/resource_hacker@v1
        with:
          exe-path: 'path/to/your/app.exe'
          icon-path: 'path/to/your/icon.ico'
```

### 高级用法

```yaml
- name: Replace icon with custom settings
  uses: overflow65537/resource_hacker@v1
  with:
    exe-path: 'MyApp.exe'
    icon-path: 'icons/custom.ico'
    output-path: 'MyApp_Modified.exe'  # 可选：输出到新文件
    resource-name: 'MAINICON'          # 可选：资源名称
    resource-type: 'ICONGROUP'         # 可选：资源类型
    resource-language: '0'             # 可选：语言ID (0=中性)
```

### 完整工作流示例

```yaml
name: Build and Customize App

on:
  release:
    types: [created]

jobs:
  customize-app:
    runs-on: windows-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      
      - name: Build application
        run: |
          # 你的构建步骤
          dotnet build -c Release
      
      - name: Replace application icon
        uses: overflow65537/resource_hacker@v1
        with:
          exe-path: 'bin/Release/MyApp.exe'
          icon-path: 'assets/icon.ico'
      
      - name: Upload artifact
        uses: actions/upload-artifact@v4
        with:
          name: customized-app
          path: 'bin/Release/MyApp.exe'
```

## 📝 输入参数

| 参数 | 必需 | 默认值 | 说明 |
|------|------|--------|------|
| `exe-path` | ✅ | - | 要修改的可执行文件路径 |
| `icon-path` | ✅ | - | 新图标文件路径（.ico） |
| `output-path` | ❌ | (同输入) | 输出文件路径，留空则覆盖原文件 |
| `resource-name` | ❌ | `MAINICON` | 资源名称 |
| `resource-type` | ❌ | `ICONGROUP` | 资源类型 |
| `resource-language` | ❌ | `0` | 语言ID（0=语言中性） |

## 📤 输出

| 输出 | 说明 |
|------|------|
| `output-file` | 修改后的可执行文件路径 |

### 使用输出示例

```yaml
- name: Replace icon
  id: icon-replace
  uses: overflow65537/resource_hacker@v1
  with:
    exe-path: 'app.exe'
    icon-path: 'icon.ico'

- name: Display output path
  run: echo "Modified file: ${{ steps.icon-replace.outputs.output-file }}"
```

## 🎯 使用场景

- 🔄 **CI/CD 自动化**：在构建流程中自动替换应用图标
- 🎨 **品牌定制**：为不同客户生成带有定制图标的应用
- 📦 **批量处理**：一次性处理多个应用程序的图标
- 🌍 **本地化**：为不同地区版本设置不同图标

## ⚖️ 许可证说明

### 本 Action 的许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件。

### Resource Hacker™ 许可证

本 Action 使用 [Resource Hacker™](https://angusj.com/resourcehacker/)，该软件：

- ✅ 是免费软件（Freeware）
- ✅ 可用于个人和商业用途
- ✅ 支持命令行自动化
- ⚠️ 不得重新分发（本 Action 通过脚本从官方网站下载）
- ⚠️ 仅可用于合法的软件修改

**重要提示**：

- 本 Action 不包含 Resource Hacker 的可执行文件
- Resource Hacker 在 Action 运行时从官方网站下载
- Resource Hacker™ 版权所有 © 1999-2025 Angus Johnson

## ⚠️ 免责声明

使用本 Action 时，请确保：

1. ✅ 您有权修改目标应用程序
2. ✅ 目标应用的许可证允许资源修改
3. ✅ 仅用于合法目的

本 Action 的作者不对任何不当使用负责。

## 🛠️ 故障排除

### 错误：找不到可执行文件

```yaml
# 确保文件路径正确，使用相对路径或绝对路径
exe-path: './build/app.exe'  # ✅ 相对路径
exe-path: 'D:/project/app.exe'  # ✅ 绝对路径
```

### 错误：图标文件无效

```yaml
# 确保使用 .ico 格式的图标文件
icon-path: 'icon.ico'  # ✅ 正确
icon-path: 'icon.png'  # ❌ 错误，需要转换为 .ico
```

### 下载 Resource Hacker 失败

如果官方网站无法访问，Action 会失败。这是预期行为，因为我们不重新分发 Resource Hacker。

## 🔗 相关链接

- [Resource Hacker 官方网站](https://angusj.com/resourcehacker/)
- [Resource Hacker 命令行文档](https://angusj.com/resourcehacker/)
- [创建 .ico 图标文件](https://www.icoconverter.com/)

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📧 联系方式

如有问题或建议，请通过 [GitHub Issues](https://github.com/overflow65537/resource_hacker/issues) 联系。

## 🙏 致谢

- [Angus Johnson](https://angusj.com/) - Resource Hacker™ 的作者

---

**注意**：Resource Hacker™ 是 Angus Johnson 的商标。本项目与 Resource Hacker 的作者没有官方关联。
