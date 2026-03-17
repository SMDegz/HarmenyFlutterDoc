# Flutter for OpenHarmony 官方文档

<div align="center">

![Flutter](https://img.shields.io/badge/Flutter-3.22+-blue.svg)
![OpenHarmony](https://img.shields.io/badge/OpenHarmony-3.0+-orange.svg)
![License](https://img.shields.io/badge/License-Apache%202.0-green.svg)
![Language](https://img.shields.io/badge/语言-中文%20%7C%20English-red.svg)

**Flutter OpenHarmony 平台适配完整文档**

[快速开始](#快速开始) • [文档导航](#文档导航) • [贡献指南](#贡献指南) • [常见问题](#常见问题)

</div>

---

## 📖 关于本文档

本文档是 Flutter 在 OpenHarmony 平台上的官方适配文档，提供从环境搭建到应用开发的全流程指导。无论你是初次接触 Flutter OpenHarmony 开发，还是需要深入了解性能优化和调试技巧，这里都能找到你需要的内容。

### 文档特色

- ✅ **全面覆盖** - 从框架介绍到实战案例，涵盖开发全流程
- 🌏 **双语支持** - 提供中文和英文两个版本
- 🎯 **实战导向** - 包含大量代码示例和场景化案例
- 🔧 **持续更新** - 跟随 Flutter 和 OpenHarmony 版本同步更新

---

## 🚀 快速开始

### 前置要求

- **开发工具**: DevEco Studio 5.0.3.300 或更高版本
- **系统要求**: OpenHarmony 3.0+ 或 HarmonyOS NEXT
- **Flutter SDK**: Flutter 3.22+ OpenHarmony 版本

### 三步上手

1. **环境搭建** - 参考 [环境搭建指导](./03_environment/openHarmony-flutter环境搭建指导.md)
2. **创建项目** - 参考 [应用构建指导](./04_development/openHarmony-flutter应用构建指导.md)
3. **运行调试** - 参考 [设备运行指导](./03_environment/OpenHarmony设备运行指导.md)

---

## 📚 文档导航

### 基础入门

| 章节 | 描述 | 链接 |
|------|------|------|
| 📚 **框架介绍** | 了解 Flutter 和 OpenHarmony 平台特性 | [查看文档](./01_framework/README.md) |
| 🏗️ **架构介绍** | 深入理解 Flutter OpenHarmony 架构设计 | [查看文档](./02_architecture/README.md) |
| ⚙️ **环境搭建** | 配置开发环境和工具链 | [查看文档](./03_environment/README.md) |

### 开发实战

| 章节 | 描述 | 链接 |
|------|------|------|
| 💻 **功能开发** | Flutter 页面、混合开发、通信机制 | [查看文档](./04_development/README.md) |
| ⚡ **性能调优** | 性能分析、内存优化、渲染优化 | [查看文档](./05_performance/README.md) |
| 🐛 **调试调测** | Dart 代码调试和原生代码调试 | [查看文档](./06_debug/README.md) |
| 🔌 **三方库接入** | 适配和使用 Flutter 三方库 | [查看文档](./07_plugin/README.md) |

### 进阶参考

| 章节 | 描述 | 链接 |
|------|------|------|
| ❓ **常见问题** | 开发过程中的常见问题和解决方案 | [查看文档](./08_FAQ/README.md) |
| 📋 **规格说明** | 项目结构和插件规格说明 | [查看文档](./09_specifications/README.md) |
| 📖 **API 文档** | Flutter 适配层 API 参考 | [查看文档](./11_flutter_api_docs/README.md) |
| 📝 **场景案例** | 实际开发中的场景化案例 | [查看文档](./Scenario_based_cases/README.md) |

---

## 🎯 核心功能指南

### 混合开发

- [如何使用 FlutterPage](./04_development/如何使用%20FlutterPage.md) - 在 OpenHarmony 应用中嵌入 Flutter 页面
- [如何使用 FlutterChannel](./04_development/如何使用Flutter与OpenHarmony通信%20FlutterChannel.md) - Flutter 与原生通信
- [如何使用 PlatformView](./04_development/如何使用PlatformView.md) - 嵌入原生视图

### 性能优化

- [性能分析定界指南](./05_performance/性能分析定界指南.md) - 定位性能瓶颈
- [帧渲染跟踪](./05_performance/性能分析-帧渲染跟踪.md) - 优化渲染性能
- [内存分析与优化](./05_performance/性能调优-内存分析与优化实践.md) - 内存优化实践

### 插件开发

- [开发 Package](./04_development/开发package.md) - 创建纯 Dart 包
- [开发 Plugin](./04_development/开发plugin.md) - 创建平台插件
- [开发 FFI Plugin](./04_development/开发FFI%20plugin.md) - 使用 FFI 调用原生代码

---

## 🌍 多语言支持

本文档提供中英文双语版本:

- **中文文档**: 大部分文档以中文为主，文件名为中文或以 `.md` 结尾
- **英文文档**: 文件名包含 `_EN` 或为英文命名，如 `README_EN.md`

### 语言切换

在每个章节的 README 文件中，都提供了对应语言版本的链接。例如:
- 中文: `01_framework/README.md`
- English: `01_framework/README_EN.md`

---

## 💡 常见问题

### 环境相关

- **Q: 如何配置 Flutter OpenHarmony 开发环境?**
  A: 参考 [环境搭建指导](./03_environment/openHarmony-flutter环境搭建指导.md)

- **Q: DevEco Studio 版本要求?**
  A: 建议使用 DevEco Studio 5.0.3.300 或更高版本

### 编译相关

- **Q: 编译时遇到错误怎么办?**
  A: 查看 [应用编译相关问题](./08_FAQ/ohos应用编译相关问题.md)

- **Q: 如何使用 --local-engine 参数?**
  A: 参考 [FAQ 文档](./08_FAQ/README.md#--local-engine-参数)

### 更多问题

查看完整的 [FAQ 文档](./08_FAQ/README.md) 获取更多帮助。

---

## 🤝 贡献指南

我们欢迎社区贡献！如果你发现文档中的问题或想要改进内容:

1. **报告问题**: 在 [Issues](https://gitcode.com/openharmony-tpc/flutter_samples/issues) 中提交问题
2. **提交改进**: Fork 仓库，修改后提交 Pull Request
3. **反馈建议**: 通过 Issue 或 PR 提供改进建议

### 问题反馈模板

提交问题时，请提供以下信息:

- IDE 版本号 (如: DevEco Studio 5.0.3.300)
- 设备信息和系统版本 (如: HUAWEI Mate 60 Pro, 3.0.0.22)
- Flutter 环境信息 (`flutter doctor -v`)
- 详细的错误日志和复现步骤

---

## 📦 相关资源

### 官方资源

- [Flutter 中文开发者网站](https://flutter.cn/)
- [OpenHarmony 官方文档](https://docs.openharmony.cn/)
- [DevEco Studio 下载](https://developer.huawei.com/consumer/cn/deveco-studio/)

### 代码仓库

- [Flutter OpenHarmony 引擎](https://gitcode.com/openharmony-tpc/flutter_flutter)
- [Flutter OpenHarmony 示例](https://gitcode.com/openharmony-tpc/flutter_samples)
- [已兼容三方库列表](https://gitcode.com/openharmony-tpc/flutter_packages)

### 社区支持

- [OpenHarmony TPC 组织](https://gitcode.com/openharmony-tpc)
- [Flutter 中文社区](https://flutter.cn/community)

---

## 📄 许可证

本文档采用 [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0) 许可证。

---

## 📮 联系我们

- **问题反馈**: [GitHub Issues](https://gitcode.com/openharmony-tpc/flutter_samples/issues)
- **技术交流**: 加入 OpenHarmony Flutter 开发者社区

---

<div align="center">

**[⬆ 返回顶部](#flutter-for-openharmony-官方文档)**

Made with ❤️ by OpenHarmony Flutter Team

</div>
