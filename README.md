# Coco - 专业影视管理刮削工具

<div align="center">
  <img src="build/icon.png" alt="Coco Logo" width="128" height="128"/>
  
  <h3>现代化的影视刮削与管理解决方案</h3>
  
  [![Version](https://img.shields.io/badge/version-1.2.27-blue.svg)](https://github.com/yrcoolio/coco/releases)
  [![License](https://img.shields.io/badge/license-MIT-green.svg)](https://opensource.org/licenses/MIT)
  [![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey.svg)](#系统要求)
</div>

## 🌟 项目简介

Coco 是一款专业的影视刮削管理应用，基于 Electron + TypeScript + Drizzle + UnoCSS + Naive UI 技术栈构建。采用现代简约设计风格，为用户提供高效、智能的影片管理体验。

### 核心价值

- 🚀 **高效刮削**：多源数据自动获取，支持批量处理
- 📁 **智能整理**：自动文件重命名与分类存储
- 🎯 **精准识别**：智能番号识别系统
- 🖼️ **完整元数据**：封面、截图、演员信息一应俱全
- ⚡ **实时监控**：文件变化自动检测处理
- 🔧 **高度定制**：丰富的配置选项满足个性化需求

## ✨ 功能特性

### 🔍 智能刮削系统

- **多源支持**：JavDB、JavBus 等主流数据源
- **智能匹配**：基于文件名自动识别番号
- **数据丰富**：演员信息、标签分类、评分等完整元数据
- **图片处理**：自动下载封面、截图、演员照片
- **断点续传**：支持失败重试与增量更新

### 📂 文件管理

- **自动整理**：根据刮削结果智能分类存储
- **文件重命名**：基于可自定义模板的文件重命名
- **路径配置**：成功/失败/未知状态的分离存储
- **实时监控**：监控指定目录，自动处理新增文件
- **批量操作**：支持大量文件的批量处理

### 🎨 用户界面

- **现代设计**：简约美观的用户界面
- **响应式布局**：适配不同屏幕尺寸
- **实时反馈**：处理进度实时显示
- **快捷操作**：右键菜单、键盘快捷键支持
- **多主题**：深色/浅色主题切换

### 🛠️ 高级功能

- **缩略图生成**：自动生成视频预览图
- **NFO文件**：兼容主流媒体库的元数据文件
- **数据导入导出**：支持数据备份与迁移
- **任务管理**：详细的任务日志与进度跟踪
- **系统集成**：与操作系统深度集成

## 📦 下载安装

### 系统要求

- **操作系统**：Windows 10+、macOS 10.15+、Ubuntu 18.04+
- **内存**：4GB RAM 或更高
- **存储空间**：500MB 可用空间
- **网络**：稳定的互联网连接

### 获取应用

1. 访问 [Releases 页面](https://github.com/yrcoolio/coco/releases)
2. 下载适合您操作系统的安装包：

#### Windows 用户

- 下载：`coco-{version}-setup.exe`
- 双击安装包，按向导完成安装
- 如提示安全警告，选择"仍要运行"

#### macOS 用户

- 下载：`coco-{version}.dmg`
- 双击挂载 DMG 文件
- 拖拽应用到 Applications 文件夹
- 如提示"未经验证的开发者"，请参考[故障排除指南](docs/TROUBLESHOOTING.md#macos-应用损坏修复)

#### Linux 用户

- 下载：`coco-{version}.AppImage`
- 添加执行权限：`chmod +x coco-*.AppImage`
- 双击运行或命令行执行：`./coco-*.AppImage`
- 如遇依赖问题，请参考[故障排除指南](docs/TROUBLESHOOTING.md#linux-安装问题)

### 首次启动配置

1. **路径设置**：配置成功、失败、未知文件的存储路径
2. **刮削配置**：选择启用的数据源和刮削选项
3. **监控设置**：设置需要监控的文件夹
4. **网络配置**：根据需要配置代理设置

## 🚀 使用指南

### 快速开始

1. **启动应用**：双击桌面图标或从开始菜单启动
2. **初始设置**：按向导完成基本配置
3. **添加文件**：
   - 拖拽文件到应用窗口
   - 启用文件夹监控自动处理
   - 手动导入指定目录

### 主要操作

#### 文件导入与刮削

```
文件监控模式（推荐）：
1. 设置 → 路径设置 → 配置监控文件夹
2. 设置 → 任务流设置 → 启用文件监控
3. 将视频文件移动到监控文件夹
4. 应用自动开始处理

手动导入模式：
1. 媒体库 → 导入文件
2. 选择要处理的文件或文件夹
3. 配置处理选项
4. 开始批量处理
```

#### 元数据管理

- **查看信息**：在媒体库中点击影片查看详细信息
- **编辑元数据**：双击信息字段进行编辑
- **重新刮削**：右键菜单选择"重新整理"
- **批量操作**：选择多个文件进行批量操作

#### 文件组织

- **自动重命名**：基于刮削结果自动重命名文件
- **智能分类**：根据演员、标签等信息分类存储
- **路径自定义**：支持自定义文件命名和目录结构模板

## ⚙️ 配置说明

### 路径配置

```
成功路径：刮削成功的文件存储位置
失败路径：刮削失败的文件存储位置
未知路径：无法识别的文件存储位置
缩略图路径：生成的缩略图存储位置
```

### 刮削配置

```
数据源：JavDB、JavBus
超时设置：网络请求超时时间
重试次数：失败后的重试次数
并发数：同时处理的文件数量
```

### 文件管理配置

```
重命名模板：自定义文件命名规则
目录模板：自定义文件夹结构
文件移动：启用/禁用文件自动移动
重复处理：如何处理重复文件
```

## 🔧 故障排除

### 常见问题

#### 应用无法启动

**现象**：双击图标后应用无响应或闪退

**解决方案**：

1. **检查系统兼容性**

   ```bash
   # Windows: 确保系统版本为 Windows 10 或更高
   # macOS: 确保系统版本为 10.15 或更高
   # Linux: 确保满足依赖要求
   ```

2. **重置应用数据**

   ```bash
   # Windows
   删除: %APPDATA%\coco

   # macOS
   删除: ~/Library/Application Support/coco

   # Linux
   删除: ~/.config/coco
   ```

3. **管理员权限运行**（Windows）

   - 右键应用图标 → "以管理员身份运行"

4. **安全软件冲突**
   - 将应用添加到杀毒软件白名单
   - 临时关闭实时保护测试

#### 刮削失败

**现象**：文件处理后显示"刮削失败"状态

**解决方案**：

1. **检查网络连接**

   ```bash
   # 测试网络连通性
   ping javdb.com
   ping javbus.com
   ```

2. **配置网络代理**

   - 设置 → 高级设置 → 网络代理
   - 配置有效的代理服务器

3. **检查文件名格式**

   ```
   支持格式：
   - PRED-123.mp4
   - [PRED-123] 标题.mp4
   - PRED123.mp4
   ```

4. **手动重试**
   - 右键文件 → "重新整理"
   - 或在导入任务中点击"重试"

#### 文件移动失败

**现象**：刮削成功但文件未移动到目标目录

**解决方案**：

1. **检查路径权限**

   ```bash
   # 确保目标目录可写
   # 检查磁盘空间是否充足
   ```

2. **检查路径配置**

   - 设置 → 路径设置 → 验证路径有效性
   - 确保路径存在且可访问

3. **手动移动**
   - 在媒体库中右键 → "打开文件夹"
   - 手动移动文件到正确位置

#### 缩略图生成失败

**现象**：视频文件无预览图显示

**解决方案**：

1. **检查 FFmpeg**

   ```bash
   # 应用会自动下载 FFmpeg
   # 如失败可手动安装并配置环境变量
   ```

2. **检查视频格式**

   ```
   支持格式：MP4, AVI, MKV, WMV, MOV 等主流格式
   ```

3. **重新生成**
   - 右键文件 → "重新整理"
   - 确保启用"生成缩略图"选项

### 应用损坏修复

#### Windows 应用损坏

**现象**：提示"应用程序无法正常启动"或文件关联异常

**修复步骤**：

1. **卸载重装**

   ```bash
   # 控制面板 → 程序和功能 → 卸载 Coco
   # 重新下载安装包进行安装
   ```

2. **清理注册表**（可选）

   ```bash
   # 使用注册表编辑器清理残留项
   # 路径：HKEY_CURRENT_USER\Software\coco
   ```

3. **重置 Windows 应用商店**（如适用）
   ```bash
   # 以管理员身份运行 PowerShell
   Get-AppxPackage -AllUsers | Foreach {Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"}
   ```

#### macOS 应用损坏

**现象**：提示"已损坏，无法打开"或"未经验证的开发者"

**修复步骤**：

1. **绕过 Gatekeeper**

   ```bash
   # 右键应用 → 打开 → 仍要打开
   # 或在终端执行：
   sudo xattr -rd com.apple.quarantine /Applications/Coco.app
   ```

2. **重新安装应用**

   ```bash
   # 删除现有应用
   rm -rf /Applications/Coco.app
   # 重新下载并安装
   ```

3. **系统完整性保护**
   ```bash
   # 如遇权限问题，临时禁用 SIP
   # 重启按 Cmd+R 进入恢复模式
   # 终端执行：csrutil disable
   ```

#### Linux 应用损坏

**现象**：启动错误或依赖缺失

**修复步骤**：

1. **检查依赖**

   ```bash
   # Ubuntu/Debian
   sudo apt-get install libnss3 libatk-bridge2.0-0 libgtk-3-0

   # CentOS/RHEL
   sudo yum install nss atk gtk3

   # Arch
   sudo pacman -S nss atk gtk3
   ```

2. **权限修复**

   ```bash
   # 添加执行权限
   chmod +x coco-*.AppImage

   # 或通过包管理器安装
   sudo dpkg -i coco-*.deb  # Debian/Ubuntu
   ```

3. **环境变量**
   ```bash
   # 添加到 ~/.bashrc 或 ~/.zshrc
   export ELECTRON_IS_DEV=0
   export NODE_ENV=production
   ```

### 性能优化

#### 提升刮削速度

1. **调整并发设置**

   - 设置 → 刮削设置 → 并发数（建议 2-4）
   - 根据网络情况调整超时时间

2. **启用缓存**

   - 设置 → 高级设置 → 启用刮削缓存
   - 定期清理过期缓存

3. **网络优化**
   - 使用稳定的网络连接
   - 配置合适的代理服务器

#### 减少资源占用

1. **限制缩略图数量**

   - 设置 → 缩略图设置 → 生成数量（建议 3-5 张）

2. **定期清理日志**

   - 日志查看器 → 清理历史日志
   - 或手动删除日志文件

3. **数据库优化**
   - 定期备份并压缩数据库
   - 清理重复或无效记录

## 🤝 反馈建议

我们重视每一个用户的反馈！

### 如何反馈

- **Bug 报告**：[提交 Bug](https://github.com/yrcoolio/coco/issues/new?template=bug_report.md)
- **功能建议**：[功能请求](https://github.com/yrcoolio/coco/issues/new?template=feature_request.md)
- **使用问题**：[问题反馈](https://github.com/yrcoolio/coco/issues)

### 反馈时请提供

- 操作系统版本和应用版本
- 详细的问题描述和复现步骤
- 相关的错误截图或日志文件
- 期望的行为或功能描述

## 📝 更新日志

### v1.2.27 (2025-06-01)

- 🎉 首个公开发布版本
- ✨ 完整的刮削和文件管理功能
- 🚀 平台支持 macOS (后续：Windows, Linux)
- 📱 现代化用户界面
- 🔧 丰富的配置选项

## 📄 许可证

本项目采用 [MIT 许可证](https://opensource.org/licenses/MIT) - 详见 [LICENSE](LICENSE) 文件

## 🙏 致谢

- [Electron](https://electronjs.org/) - 跨平台桌面应用框架
- [Vue.js](https://vuejs.org/) - 渐进式 JavaScript 框架
- [Naive UI](https://naiveui.com/) - Vue 3 组件库
- [JavDB](https://javdb.com/) - 数据源支持
- [JavBus](https://javbus.com/) - 数据源支持

## 📞 联系我们

- **GitHub Issues**: [问题反馈](https://github.com/yrcoolio/coco/issues)
- **功能建议**: [功能请求](https://github.com/yrcoolio/coco/issues/new?template=feature_request.md)
- **Bug 报告**: [Bug 反馈](https://github.com/yrcoolio/coco/issues/new?template=bug_report.md)

## 📖 相关文档

- [故障排除指南](docs/TROUBLESHOOTING.md) - 详细的问题解决方案
- [发布说明](https://github.com/yrcoolio/coco/releases) - 版本更新历史

---

<div align="center">
  <p>⭐ 如果这个项目对你有帮助，请给它一个星标支持！</p>
  <p>Made with ❤️ by the Coco Team</p>
</div>
