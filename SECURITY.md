# 安全和合规说明

## 🔒 安全考虑

### Resource Hacker 下载

本 Action 在运行时从 Resource Hacker 的官方网站下载软件：

- **下载源**: `https://angusj.com/resourcehacker/resource_hacker.zip`
- **验证**: Action 会验证下载的文件包含 `ResourceHacker.exe`
- **临时存储**: 下载的文件存储在 `$env:TEMP` 临时目录
- **自动清理**: 执行完成后自动删除所有临时文件

### 潜在风险

1. **网络依赖**
   - Action 需要访问外部网站下载 Resource Hacker
   - 如果官方网站不可用，Action 将失败
   - 这是有意设计，以符合许可证要求

2. **可执行文件修改**
   - 本 Action 会修改 Windows 可执行文件
   - 请确保您有权修改目标文件
   - 建议在修改前备份原始文件

3. **第三方软件**
   - Resource Hacker 是第三方软件
   - 本项目不对 Resource Hacker 的行为负责
   - 请阅读 Resource Hacker 的许可证和文档

## ⚖️ 许可证合规

### Resource Hacker™ 许可证要求

根据 Resource Hacker 的许可证条款：

#### ✅ 允许的操作

1. **免费使用**: Resource Hacker 是免费软件，可以免费使用
2. **命令行自动化**: 明确支持通过命令行和脚本自动化
3. **个人和商业用途**: 可用于合法的商业项目

#### ❌ 禁止的操作

1. **重新分发**: 
   > "This software is not to be distributed via any website domain or any other media without the prior written approval of the copyright owner."
   **本 Action 的解决方案**: 
   - ✅ 不包含 Resource Hacker 可执行文件
   - ✅ 运行时从官方网站下载
   - ✅ 下载后存储在临时目录
   - ✅ 执行完成后自动删除

2. **非法使用**:
   > "This software is not to be used in any way to illegally modify software."
   
   **用户责任**:
   - ⚠️ 用户必须确保有权修改目标软件
   - ⚠️ 用户必须遵守目标软件的许可证
   - ⚠️ 仅用于合法目的

### 本项目许可证

本 GitHub Action 项目采用 **MIT 许可证**，允许：
- ✅ 商业使用
- ✅ 修改
- ✅ 分发
- ✅ 私人使用

**但是**，使用本 Action 时仍需遵守 Resource Hacker 的许可证条款。

## 🎯 合规使用指南

### ✅ 合规场景

1. **自有应用程序**
   ```yaml
   # 为您自己开发的应用程序替换图标
   - uses: overflow65537/resource_hacker@v1
     with:
       exe-path: 'my-own-app.exe'
       icon-path: 'my-icon.ico'
   ```

2. **开源项目**
   ```yaml
   # 为开源项目自定义图标（如果许可证允许）
   # 确保检查项目许可证
   - uses: overflow65537/resource_hacker@v1
     with:
       exe-path: 'open-source-app.exe'
       icon-path: 'custom-icon.ico'
   ```

3. **客户定制**
   ```yaml
   # 为客户创建定制版本（在授权情况下）
   - uses: overflow65537/resource_hacker@v1
     with:
       exe-path: 'client-app.exe'
       icon-path: 'client-branding.ico'
   ```

### ❌ 不合规场景

1. **未经授权的第三方软件**
   ```yaml
   # ❌ 不要修改未经授权的商业软件
   - uses: overflow65537/resource_hacker@v1
     with:
       exe-path: 'third-party-commercial.exe'  # 未经许可
       icon-path: 'custom.ico'
   ```

2. **恶意目的**
   ```yaml
   # ❌ 不要用于伪装或欺骗
   - uses: overflow65537/resource_hacker@v1
     with:
       exe-path: 'malware.exe'  # 非法
       icon-path: 'trusted-app-icon.ico'
   ```

## 📋 使用前检查清单

在使用本 Action 之前，请确认：

- [ ] 我有权修改目标可执行文件
- [ ] 目标软件的许可证允许资源修改
- [ ] 我了解 Resource Hacker 的许可证条款
- [ ] 我将仅用于合法目的
- [ ] 我已阅读并理解本文档

## 🛡️ 最佳实践

### 1. 备份原始文件

```yaml
- name: Backup original file
  shell: powershell
  run: |
    Copy-Item 'app.exe' 'app.exe.backup'

- name: Replace icon
  uses: overflow65537/resource_hacker@v1
  with:
    exe-path: 'app.exe'
    icon-path: 'icon.ico'
```

### 2. 使用输出路径（推荐）

```yaml
# 不覆盖原文件，创建新文件
- name: Replace icon
  uses: overflow65537/resource_hacker@v1
  with:
    exe-path: 'app.exe'
    icon-path: 'icon.ico'
    output-path: 'app-customized.exe'  # 保留原文件
```

### 3. 验证修改结果

```yaml
- name: Verify modified file
  shell: powershell
  run: |
    if (Test-Path 'app-customized.exe') {
      $hash = Get-FileHash 'app-customized.exe' -Algorithm SHA256
      Write-Host "SHA256: $($hash.Hash)"
    }
```

### 4. 文档化修改

在项目文档中说明：
- 使用了哪些第三方工具
- 修改了哪些资源
- 合法性依据

## 🔍 透明度

本项目完全开源，所有代码可在 GitHub 上查看：
- **Action 定义**: `action.yml`
- **工作流**: `.github/workflows/`
- **文档**: `README.md`, `SECURITY.md`

如果您发现任何安全问题，请通过 GitHub Issues 报告。

## 📞 联系方式

如有安全或合规方面的疑问：
- **GitHub Issues**: [创建 Issue](https://github.com/overflow65537/resource_hacker/issues)
- **安全问题**: 请通过 GitHub 的安全报告功能报告

## 📚 相关资源

- [Resource Hacker 官方网站](https://angusj.com/resourcehacker/)
- [Resource Hacker 许可证](https://angusj.com/resourcehacker/#license)
- [GitHub Actions 安全最佳实践](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions)

## 免责声明

本文档提供的信息仅供参考。最终的合规性和合法性由用户负责。本项目作者不对任何滥用或违规使用承担责任。

使用本 Action 即表示您同意：
1. 遵守所有适用的法律法规
2. 遵守 Resource Hacker 的许可证条款
3. 仅将其用于合法目的
4. 对您的使用承担全部责任

---

最后更新: 2025年10月20日
