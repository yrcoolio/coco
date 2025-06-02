# Coco 故障排除指南

本文档提供详细的故障排除步骤，帮助您解决使用 Coco 时可能遇到的各种问题。

## 📋 目录

- [安装问题](#安装问题)
- [启动问题](#启动问题)
- [应用损坏](#应用损坏)
- [刮削问题](#刮削问题)
- [文件处理问题](#文件处理问题)
- [性能问题](#性能问题)
- [网络问题](#网络问题)
- [数据库问题](#数据库问题)
- [日志分析](#日志分析)
- [重置与恢复](#重置与恢复)

## 🔧 安装问题

### Windows 安装失败

**问题描述**：安装程序无法正常运行或提示错误

**解决步骤**：

1. **管理员权限安装**

   ```powershell
   # 右键安装包 → "以管理员身份运行"
   ```

2. **检查系统版本**

   ```powershell
   # Windows 10 版本 1903 或更高
   winver
   ```

3. **清理旧版本残留**

   ```powershell
   # 卸载旧版本
   # 删除 %APPDATA%\coco
   # 删除 %LOCALAPPDATA%\coco
   ```

4. **禁用杀毒软件**
   - 临时禁用实时保护
   - 将安装包添加到白名单

### macOS 安装问题

**问题描述**：DMG 无法挂载或应用无法安装

**解决步骤**：

1. **绕过安全限制**

   ```bash
   # 允许任何来源的应用
   sudo spctl --master-disable

   # 安装完成后重新启用
   sudo spctl --master-enable
   ```

2. **清除隔离属性**

   ```bash
   # 下载完成后执行
   xattr -c ~/Downloads/coco-*.dmg
   ```

3. **手动安装**
   ```bash
   # 如果拖拽安装失败
   sudo cp -R /Volumes/Coco/Coco.app /Applications/
   ```

### Linux 安装问题

**问题描述**：AppImage 无法运行或依赖缺失

**解决步骤**：

1. **安装依赖库**

   ```bash
   # Ubuntu/Debian
   sudo apt update
   sudo apt install libfuse2 libnss3 libatk-bridge2.0-0 libgtk-3-0 \
                    libgdk-pixbuf2.0-0 libdrm2 libxcomposite1 libxdamage1 \
                    libxrandr2 libgbm1 libxss1 libasound2

   # CentOS/RHEL
   sudo yum install fuse-libs nss atk gtk3 gdk-pixbuf2 \
                    libdrm libXcomposite libXdamage libXrandr mesa-libgbm \
                    libXScrnSaver alsa-lib

   # Arch Linux
   sudo pacman -S fuse2 nss atk gtk3 gdk-pixbuf2 \
                  libdrm libxcomposite libxdamage libxrandr mesa \
                  libxss alsa-lib
   ```

2. **添加执行权限**

   ```bash
   chmod +x coco-*.AppImage
   ```

3. **使用 DEB 包安装**
   ```bash
   # 如果 AppImage 不工作
   sudo dpkg -i coco-*.deb
   sudo apt-get install -f  # 修复依赖
   ```

## 🚀 启动问题

### 应用无法启动

**问题描述**：双击图标后无反应或闪退

**诊断步骤**：

1. **命令行启动**（获取错误信息）

   ```bash
   # Windows
   "C:\Users\{用户名}\AppData\Local\Programs\coco\coco.exe"

   # macOS
   /Applications/Coco.app/Contents/MacOS/Coco

   # Linux
   ./coco-*.AppImage
   ```

2. **检查日志文件**

   ```bash
   # Windows
   %APPDATA%\coco\logs\

   # macOS
   ~/Library/Application Support/coco/logs/

   # Linux
   ~/.config/coco/logs/
   ```

**常见解决方案**：

1. **重置配置文件**

   ```bash
   # 重命名或删除配置目录
   # Windows: %APPDATA%\coco
   # macOS: ~/Library/Application Support/coco
   # Linux: ~/.config/coco
   ```

2. **检查端口冲突**

   ```bash
   # 检查是否有其他实例运行
   # Windows: tasklist | findstr coco
   # macOS/Linux: ps aux | grep coco
   ```

3. **清理进程**
   ```bash
   # 结束所有相关进程
   # Windows: taskkill /f /im coco.exe
   # macOS/Linux: killall coco
   ```

### 权限问题

**问题描述**：提示权限不足或无法访问文件

**解决步骤**：

1. **Windows**

   ```powershell
   # 以管理员身份运行
   # 右键图标 → "以管理员身份运行"

   # 修改文件夹权限
   icacls "C:\Program Files\coco" /grant Users:F /T
   ```

2. **macOS**

   ```bash
   # 授予完全磁盘访问权限
   # 系统偏好设置 → 安全性与隐私 → 隐私 → 完全磁盘访问权限

   # 修复权限
   sudo chown -R $(whoami) ~/Library/Application\ Support/coco
   ```

3. **Linux**

   ```bash
   # 修改权限
   chmod -R 755 ~/.config/coco

   # SELinux 问题（如适用）
   setsebool -P use_execstack 1
   ```

## 💔 应用损坏

### Windows 应用损坏修复

**症状识别**：

- 应用程序错误对话框
- 文件关联失效
- 功能异常或崩溃
- DLL 错误

**修复步骤**：

1. **使用系统文件检查器**

   ```powershell
   # 以管理员身份运行 PowerShell
   sfc /scannow
   DISM /Online /Cleanup-Image /RestoreHealth
   ```

2. **重新注册 DLL**

   ```powershell
   # 重新注册系统 DLL
   regsvr32 /u /s comctl32.dll
   regsvr32 /s comctl32.dll
   ```

3. **修复应用程序**

   ```powershell
   # 控制面板 → 程序和功能 → Coco → 修复
   # 或卸载后重新安装
   ```

4. **清理注册表**

   ```powershell
   # 使用 regedit 删除以下键值：
   # HKEY_CURRENT_USER\Software\coco
   # HKEY_LOCAL_MACHINE\SOFTWARE\coco
   ```

5. **重置 Windows 应用**
   ```powershell
   Get-AppxPackage -AllUsers | Foreach {
       Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"
   }
   ```

### macOS 应用损坏修复

**症状识别**：

- "应用程序已损坏"提示
- "无法验证开发者"错误
- 应用无响应或异常退出

**修复步骤**：

1. **移除隔离属性**

   ```bash
   # 方法一：单个应用
   sudo xattr -rd com.apple.quarantine /Applications/Coco.app

   # 方法二：批量清理
   sudo xattr -rd com.apple.quarantine /Applications/*.app
   ```

2. **重新签名应用**

   ```bash
   # 如果有开发者账户
   codesign --force --deep --sign - /Applications/Coco.app
   ```

3. **绕过 Gatekeeper**

   ```bash
   # 方法一：系统偏好设置
   # 系统偏好设置 → 安全性与隐私 → 通用 → 允许从以下位置下载的应用

   # 方法二：命令行
   sudo spctl --master-disable
   # 使用后记得重新启用
   sudo spctl --master-enable
   ```

4. **重建 LaunchServices 数据库**

   ```bash
   /System/Library/Frameworks/CoreServices.framework/Frameworks/LaunchServices.framework/Support/lsregister -kill -r -domain local -domain system -domain user
   ```

5. **修复磁盘权限**
   ```bash
   # 磁盘工具 → First Aid
   # 或命令行
   sudo diskutil repairPermissions /
   ```

### Linux 应用损坏修复

**症状识别**：

- Segmentation fault 错误
- 库文件缺失或版本不兼容
- 图形界面无法显示

**修复步骤**：

1. **检查依赖库**

   ```bash
   # 查看缺失的依赖
   ldd coco-*.AppImage

   # 检查特定库
   ldconfig -p | grep libname
   ```

2. **修复损坏的库**

   ```bash
   # Ubuntu/Debian
   sudo apt-get update
   sudo apt-get install --reinstall libc6-dev

   # CentOS/RHEL
   sudo yum reinstall glibc-devel

   # Arch Linux
   sudo pacman -S glibc
   ```

3. **重建符号链接**

   ```bash
   # 重建 ld 缓存
   sudo ldconfig

   # 手动创建符号链接（如需要）
   sudo ln -s /usr/lib/x86_64-linux-gnu/libssl.so.1.1 /usr/lib/x86_64-linux-gnu/libssl.so.1.0.0
   ```

4. **环境变量修复**

   ```bash
   # 添加到 ~/.bashrc 或 ~/.zshrc
   export LD_LIBRARY_PATH=/usr/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH
   export ELECTRON_IS_DEV=0
   ```

5. **AppImage 修复**

   ```bash
   # 提取 AppImage 内容
   ./coco-*.AppImage --appimage-extract

   # 手动运行
   ./squashfs-root/coco
   ```

## 🔍 刮削问题

### 刮削完全失败

**问题描述**：所有文件都显示刮削失败

**解决步骤**：

1. **网络连接检查**

   ```bash
   # 测试数据源连通性
   ping javdb.com
   ping javbus.com

   # 测试 DNS 解析
   nslookup javdb.com
   ```

2. **代理配置**

   ```json
   // 设置 → 高级设置 → 网络代理
   {
   	"proxy": {
   		"type": "http",
   		"host": "127.0.0.1",
   		"port": 7890
   	}
   }
   ```

3. **防火墙设置**

   ```bash
   # Windows 防火墙
   # 控制面板 → 系统和安全 → Windows Defender 防火墙 → 允许应用通过防火墙

   # macOS 防火墙
   # 系统偏好设置 → 安全性与隐私 → 防火墙 → 防火墙选项

   # Linux iptables
   sudo iptables -A OUTPUT -p tcp --dport 80,443 -j ACCEPT
   ```

### 部分文件刮削失败

**问题描述**：某些文件无法识别或刮削失败

**解决步骤**：

1. **文件名格式检查**

   ```javascript
   // 支持的格式示例
   'PRED-123.mp4'
   '[PRED-123] Title.mp4'
   'PRED123.mp4'
   'pred-123.mp4'
   ```

2. **手动编辑番号**

   - 在媒体库中右键文件
   - 选择"编辑信息"
   - 修改"番号"字段
   - 点击"重新刮削"

3. **调整刮削设置**
   ```json
   // 设置 → 刮削设置
   {
   	"timeout": 30000, // 增加超时时间
   	"retryCount": 3, // 增加重试次数
   	"detailLevel": "full" // 使用完整模式
   }
   ```

### 图片下载失败

**问题描述**：刮削成功但图片无法下载

**解决步骤**：

1. **网络质量检查**

   ```bash
   # 测试下载速度
   curl -o /dev/null -s -w "%{speed_download}\n" https://example.com/image.jpg
   ```

2. **User-Agent 设置**

   ```javascript
   // 某些站点需要特定的 User-Agent
   // 应用会自动处理，但可在设置中调整
   ```

3. **跳过图片验证**
   ```json
   // 设置 → 刮削设置 → 高级选项
   {
   	"skipImageValidation": true
   }
   ```

## 📁 文件处理问题

### 文件移动失败

**问题描述**：刮削成功但文件未移动到目标位置

**诊断步骤**：

1. **权限检查**

   ```bash
   # 检查目标目录权限
   # Windows: 右键 → 属性 → 安全
   # macOS/Linux: ls -la /target/directory
   ```

2. **磁盘空间检查**

   ```bash
   # Windows: dir
   # macOS/Linux: df -h
   ```

3. **路径验证**
   ```javascript
   // 确保路径存在且可写
   // 设置 → 路径设置 → 测试路径
   ```

**解决方案**：

1. **手动移动**

   ```bash
   # 在媒体库中右键 → "打开文件夹"
   # 手动移动到正确位置
   ```

2. **修复权限**

   ```bash
   # Windows
   icacls "目标路径" /grant Users:F /T

   # macOS
   sudo chown -R $(whoami) /target/path

   # Linux
   chmod -R 755 /target/path
   ```

### 重复文件处理

**问题描述**：重复文件导致处理失败

**解决步骤**：

1. **配置重复处理策略**

   ```json
   // 设置 → 文件管理 → 重复文件处理
   {
   	"duplicateHandling": "skip", // 跳过
   	"duplicateHandling": "overwrite", // 覆盖
   	"duplicateHandling": "rename" // 重命名
   }
   ```

2. **清理重复记录**
   ```sql
   -- 在数据库中清理重复记录
   -- 工具 → 数据库管理 → 清理重复项
   ```

### 文件名编码问题

**问题描述**：文件名包含特殊字符导致处理失败

**解决步骤**：

1. **文件名清理**

   ```javascript
   // 应用会自动清理非法字符
   // 可在设置中配置清理规则
   ```

2. **编码转换**
   ```bash
   # 转换文件名编码
   # Linux: convmv -f gbk -t utf8 filename
   ```

## 🚀 性能问题

### 应用运行缓慢

**问题描述**：界面响应慢或处理速度慢

**优化步骤**：

1. **减少并发数**

   ```json
   // 设置 → 刮削设置 → 并发控制
   {
   	"globalMax": 2, // 减少全局并发
   	"perSourceMax": 1 // 减少单源并发
   }
   ```

2. **清理缓存**

   ```bash
   # 清理应用缓存
   # 设置 → 高级设置 → 清理缓存
   ```

3. **数据库优化**

   ```sql
   -- 定期压缩数据库
   -- 工具 → 数据库管理 → 压缩数据库
   ```

4. **限制缩略图**
   ```json
   // 设置 → 缩略图设置
   {
   	"generateCount": 3, // 减少生成数量
   	"quality": 70 // 降低质量
   }
   ```

### 内存占用过高

**问题描述**：应用占用大量内存

**解决步骤**：

1. **重启应用**

   ```bash
   # 定期重启释放内存
   ```

2. **调整缓存大小**

   ```json
   // 设置 → 高级设置 → 缓存配置
   {
   	"maxSize": 100, // 减少缓存大小(MB)
   	"ttl": 1 // 减少缓存时间(小时)
   }
   ```

3. **关闭不必要功能**
   ```json
   // 临时关闭一些功能
   {
   	"enableThumbnails": false,
   	"enablePreview": false
   }
   ```

## 🌐 网络问题

### 连接超时

**问题描述**：网络请求频繁超时

**解决步骤**：

1. **增加超时时间**

   ```json
   // 设置 → 刮削设置
   {
   	"timeout": 60000 // 增加到60秒
   }
   ```

2. **检查网络质量**

   ```bash
   # 测试延迟
   ping -c 10 javdb.com

   # 测试带宽
   speedtest-cli
   ```

3. **更换DNS**
   ```bash
   # 使用公共DNS
   # 8.8.8.8, 1.1.1.1, 114.114.114.114
   ```

### 代理配置问题

**问题描述**：代理设置后仍无法访问

**解决步骤**：

1. **验证代理可用性**

   ```bash
   # 测试代理连接
   curl --proxy http://proxy:port http://httpbin.org/ip
   ```

2. **检查代理认证**

   ```json
   // 如果代理需要认证
   {
   	"proxy": {
   		"type": "http",
   		"host": "proxy.example.com",
   		"port": 8080,
   		"username": "user",
   		"password": "pass"
   	}
   }
   ```

3. **尝试不同代理类型**
   ```json
   // SOCKS5 代理
   {
   	"proxy": {
   		"type": "socks5",
   		"host": "127.0.0.1",
   		"port": 1080
   	}
   }
   ```

## 💾 数据库问题

### 数据库损坏

**问题描述**：应用提示数据库错误或无法读取数据

**修复步骤**：

1. **备份现有数据库**

   ```bash
   # 复制数据库文件
   # Windows: %APPDATA%\coco\database.db
   # macOS: ~/Library/Application Support/coco/database.db
   # Linux: ~/.config/coco/database.db
   ```

2. **数据库完整性检查**

   ```sql
   -- 使用内置工具检查
   -- 工具 → 数据库管理 → 完整性检查
   ```

3. **重建数据库**

   ```bash
   # 删除损坏的数据库文件
   # 重启应用会自动创建新数据库
   ```

4. **从备份恢复**
   ```bash
   # 恢复最近的备份
   # 工具 → 数据库管理 → 恢复备份
   ```

### 数据丢失

**问题描述**：媒体库数据消失或不完整

**恢复步骤**：

1. **检查备份**

   ```bash
   # 查找自动备份
   # 设置 → 高级设置 → 备份管理
   ```

2. **重新扫描**

   ```bash
   # 重新扫描媒体库
   # 媒体库 → 重新扫描
   ```

3. **导入数据**
   ```bash
   # 从导出文件恢复
   # 工具 → 数据管理 → 导入数据
   ```

## 📊 日志分析

### 查看应用日志

**日志位置**：

```bash
# Windows
%APPDATA%\coco\logs\

# macOS
~/Library/Application Support/coco/logs/

# Linux
~/.config/coco/logs/
```

**重要日志文件**：

- `main.log` - 主进程日志
- `renderer.log` - 渲染进程日志
- `scraper.log` - 刮削相关日志
- `import.log` - 导入任务日志

**日志级别**：

- `ERROR` - 错误信息
- `WARN` - 警告信息
- `INFO` - 一般信息
- `DEBUG` - 调试信息

### 常见错误分析

1. **网络相关错误**

   ```
   ERROR: ECONNREFUSED - 连接被拒绝
   ERROR: ETIMEDOUT - 连接超时
   ERROR: ENOTFOUND - 域名解析失败
   ```

2. **文件系统错误**

   ```
   ERROR: EACCES - 权限不足
   ERROR: ENOENT - 文件不存在
   ERROR: ENOSPC - 磁盘空间不足
   ```

3. **数据库错误**
   ```
   ERROR: SQLITE_CORRUPT - 数据库损坏
   ERROR: SQLITE_LOCKED - 数据库被锁定
   ```

## 🔄 重置与恢复

### 完全重置应用

**警告**：此操作将删除所有数据和设置

**步骤**：

1. **关闭应用**

   ```bash
   # 确保应用完全关闭
   # Windows: taskkill /f /im coco.exe
   # macOS/Linux: killall coco
   ```

2. **删除应用数据**

   ```bash
   # Windows
   rmdir /s "%APPDATA%\coco"
   rmdir /s "%LOCALAPPDATA%\coco"

   # macOS
   rm -rf ~/Library/Application\ Support/coco
   rm -rf ~/Library/Preferences/com.electron.coco.plist

   # Linux
   rm -rf ~/.config/coco
   rm -rf ~/.local/share/coco
   ```

3. **清理缓存**

   ```bash
   # Windows
   rmdir /s "%TEMP%\coco"

   # macOS
   rm -rf ~/Library/Caches/coco

   # Linux
   rm -rf ~/.cache/coco
   ```

4. **重新启动应用**
   - 应用将以全新状态启动
   - 需要重新进行初始配置

### 配置备份与恢复

**备份配置**：

```bash
# 复制配置文件
# Windows: %APPDATA%\coco\config.json
# macOS: ~/Library/Application Support/coco/config.json
# Linux: ~/.config/coco/config.json
```

**恢复配置**：

```bash
# 将备份的配置文件复制回原位置
# 重启应用生效
```

## 📞 获取帮助

如果以上步骤无法解决您的问题，请：

1. **收集信息**：

   - 操作系统版本
   - 应用版本
   - 错误信息截图
   - 相关日志文件

2. **提交问题**：

   - [GitHub Issues](https://github.com/yrcoolio/coco/issues)
   - 详细描述问题和复现步骤

3. **紧急问题**：
   - 查看 [常见问题 FAQ](https://github.com/yrcoolio/coco/wiki/FAQ)
   - 搜索已有的 Issue

---

_最后更新时间：2025年6月1
