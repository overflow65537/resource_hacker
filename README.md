# Resource Hacker Icon Replacer Action

**English | [简体中文](README.zh-CN.md)**

[![GitHub release](https://img.shields.io/github/v/release/overflow65537/resource_hacker)](https://github.com/overflow65537/resource_hacker/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

🎨 A GitHub Action to automatically replace Windows application icons. This action downloads and uses [Resource Hacker™](https://angusj.com/resourcehacker/) automatically.

## ✨ Features

- 🚀 **Automated**: No manual installation of Resource Hacker required - the action downloads it automatically
- 🎯 **Simple**: Just provide an exe file and an ico icon
- 🔧 **Flexible**: Support for custom resource names, types, and languages
- 📦 **Lightweight**: No third-party executables included in the repository
- ✅ **Reliable**: Complete error checking and logging

## 📋 Requirements

- Windows runner environment (use `runs-on: windows-latest`)
- Valid `.ico` icon file
- Target Windows executable file (`.exe`)

## 🚀 Usage

### Basic Usage

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

### Advanced Usage

```yaml
- name: Replace icon with custom settings
  uses: overflow65537/resource_hacker@v1
  with:
    exe-path: 'MyApp.exe'
    icon-path: 'icons/custom.ico'
    output-path: 'MyApp_Modified.exe'  # Optional: output to new file
    resource-name: 'MAINICON'          # Optional: resource name
    resource-type: 'ICONGROUP'         # Optional: resource type
    resource-language: '0'             # Optional: language ID (0=neutral)
```

### Complete Workflow Example

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
          # Your build steps
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

## 📝 Inputs

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `exe-path` | ✅ | - | Path to the executable file to modify |
| `icon-path` | ✅ | - | Path to the new icon file (.ico) |
| `output-path` | ❌ | (same as input) | Output file path, leave empty to overwrite original |
| `resource-name` | ❌ | `MAINICON` | Resource name |
| `resource-type` | ❌ | `ICONGROUP` | Resource type |
| `resource-language` | ❌ | `0` | Language ID (0=language neutral) |

## 📤 Outputs

| Output | Description |
|--------|-------------|
| `output-file` | Path to the modified executable file |

### Output Usage Example

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

## 🎯 Use Cases

- 🔄 **CI/CD Automation**: Automatically replace application icons in build pipelines
- 🎨 **Brand Customization**: Generate applications with customized icons for different clients
- 📦 **Batch Processing**: Process icons for multiple applications at once
- 🌍 **Localization**: Set different icons for different regional versions

## ⚖️ License

### This Action's License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### Resource Hacker™ License

This action uses [Resource Hacker™](https://angusj.com/resourcehacker/), which is:

- ✅ Freeware
- ✅ Available for personal and commercial use
- ✅ Supports command-line automation
- ⚠️ Cannot be redistributed (this action downloads it from the official website via script)
- ⚠️ Must only be used for legal software modification

**Important Notes**:

- This action does not include Resource Hacker executables
- Resource Hacker is downloaded from the official website at runtime
- Resource Hacker™ © 1999-2025 Angus Johnson

## ⚠️ Disclaimer

When using this action, please ensure:

1. ✅ You have the right to modify the target application
2. ✅ The target application's license allows resource modification
3. ✅ You use it for legal purposes only

The author of this action is not responsible for any misuse.

## 🛠️ Troubleshooting

### Error: Executable file not found

```yaml
# Ensure the file path is correct, use relative or absolute paths
exe-path: './build/app.exe'  # ✅ Relative path
exe-path: 'D:/project/app.exe'  # ✅ Absolute path
```

### Error: Invalid icon file

```yaml
# Ensure you use .ico format icon files
icon-path: 'icon.ico'  # ✅ Correct
icon-path: 'icon.png'  # ❌ Wrong, needs conversion to .ico
```

### Resource Hacker download failed

If the official website is unavailable, the action will fail. This is expected behavior as we do not redistribute Resource Hacker.

## 🔗 Related Links

- [Resource Hacker Official Website](https://angusj.com/resourcehacker/)
- [Resource Hacker Command Line Documentation](https://angusj.com/resourcehacker/)
- [Create .ico Icon Files](https://www.icoconverter.com/)

## 🤝 Contributing

Issues and Pull Requests are welcome!

## 📧 Contact

For questions or suggestions, please contact via [GitHub Issues](https://github.com/overflow65537/resource_hacker/issues).

## 🙏 Acknowledgments

- [Angus Johnson](https://angusj.com/) - Author of Resource Hacker™

---

**Note**: Resource Hacker™ is a trademark of Angus Johnson. This project is not officially affiliated with the author of Resource Hacker.
