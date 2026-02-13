# AI Plugin Manager

> 统一管理你的 AI 编程助手插件，告别重复安装与存储浪费

## 为什么需要这个工具？

在 AI 辅助编程时代，越来越多的开发者同时使用多个 AI 编辑器：
- **Cursor** - AI 原生代码编辑器
- **VS Code + Copilot** - 微软官方 AI 助手
- **Roo Code** - 开源 AI 编程工具
- **Windsurf**、**Trae** 等新兴工具...

每个编辑器都维护自己的插件目录，导致：
- 🔄 **重复安装**：同一个插件在不同编辑器中各存一份
- 💾 **磁盘浪费**：Copilot、Cline 等大型插件动辄数百 MB，重复存储占用大量空间
- 📦 **版本混乱**：不同编辑器可能安装了不同版本，难以统一管理
- 🛠️ **同步困难**：新装一个编辑器，需要重新安装所有插件

**AI Plugin Manager 就是来解决这个问题的**——类似 Node.js 的 pnpm，通过符号链接实现插件共享，一处安装，处处可用。

## 核心功能

### 🔍 智能发现
自动扫描系统中已安装的 VS Code 系编辑器及其插件，无需手动配置。

### 📊 重复检测
分析所有编辑器的插件，识别重复安装，计算浪费的磁盘空间。

### 🔗 符号链接管理
- 创建符号链接替代实际文件，多个编辑器共享同一份插件
- 支持批量链接/取消链接
- 自动验证链接有效性，修复损坏的链接

### 🚀 一键优化
- 自动生成优化方案
- 保留最新/最大的版本作为主副本
- 批量执行去重操作

## 使用场景

| 场景 | 传统方式 | AI Plugin Manager |
|------|----------|-------------------|
| 新装 Cursor，想用已有的 Copilot | 重新下载安装 | 一键链接，秒级完成 |
| 5 个编辑器都装了 Cline | 占用 5 × 200MB = 1GB | 只需 200MB |
| 统一插件版本 | 手动逐个更新 | 集中管理，一处更新 |
| 检查插件重复 | 无法直观看到 | 自动检测并报告 |

## 支持的编辑器

- ✅ Cursor
- ✅ VS Code
- ✅ Roo Code
- ✅ Windsurf
- ✅ Trae
- 🔧 可扩展支持更多基于 VS Code 的编辑器

## 安装

### 从源码编译

```bash
# 克隆项目
git clone https://github.com/yourusername/AIPluginManager.git
cd AIPluginManager

# 生成 Xcode 项目
brew install xcodegen
xcodegen generate

# 编译
xcodebuild -project AIPluginManager.xcodeproj -scheme AIPluginManager -configuration Release build
```

## 快速开始

1. **扫描编辑器** - 自动发现已安装的 AI 编辑器
2. **检测重复** - 分析插件重复情况，查看可节省的空间
3. **执行优化** - 一键创建符号链接，释放磁盘空间

## 技术栈

- **UI 框架**: SwiftUI
- **语言**: Swift
- **项目生成**: XcodeGen
- **存储**: SQLite + UserDefaults

## 工作原理

```
传统方式:
┌─────────┐    ┌─────────┐    ┌─────────┐
│ Cursor  │    │ VS Code │    │ Roo Code│
│ plugins │    │ plugins │    │ plugins │
│  (200MB)│    │  (200MB)│    │  (200MB)│
└────┬────┘    └────┬────┘    └────┬────┘
     │              │              │
     └──────────────┴──────────────┘
              总计: 600MB

AI Plugin Manager:
                    ┌─────────────┐
                    │ Plugin Store│
                    │   (200MB)   │
                    └──────┬──────┘
           ┌───────────────┼───────────────┐
           │               │               │
           ▼               ▼               ▼
     ┌─────────┐    ┌─────────┐    ┌─────────┐
     │ Cursor  │    │ VS Code │    │ Roo Code│
     │  link → │    │  link → │    │  link → │
     └─────────┘    └─────────┘    └─────────┘
              总计: 200MB
```

## License

MIT
