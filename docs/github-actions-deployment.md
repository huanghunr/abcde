# GitHub Actions 部署指南

## 概述

本项目使用 GitHub Actions 自动构建和部署 Universal Jar 文件。工作流程文件位于 `.github/workflows/universal-jar.yml`。

## 构建触发条件

工作流程会在以下情况下自动运行：

1. **推送到 main 分支** - 构建最新版本并上传为 Artifacts
2. **提交 Pull Request 到 main 分支** - 验证构建是否成功
3. **推送版本标签** (格式：`v*.*.*`) - 构建并创建 GitHub Release

## 如何创建发布版本

要创建新的发布版本，请按以下步骤操作：

1. 确保代码已经合并到 main 分支
2. 创建版本标签（例如 v1.0.0）：
   ```bash
   git tag v1.0.0
   ```
3. 推送标签到 GitHub：
   ```bash
   git push origin v1.0.0
   ```

GitHub Actions 会自动：
- 构建 Universal Jar
- 创建 GitHub Release
- 上传 JAR 文件到 Release
- 生成发布说明

## 下载构建文件

### 稳定版本
访问 [GitHub Releases](https://github.com/Yricky/abcde/releases) 页面下载已发布的稳定版本。

### 最新构建
访问 [GitHub Actions](https://github.com/Yricky/abcde/actions) 页面，选择最新的成功构建，在 Artifacts 部分下载 `universal-jar`。

## 工作流程详情

### 构建环境
- 操作系统：Ubuntu Latest
- JDK 版本：17
- Gradle：使用项目自带的 Gradle Wrapper

### 构建命令
```bash
./gradlew :abcdecoder:packageReleaseUberJarForCurrentOS -Puniversal
```

`-Puniversal` 参数确保构建包含所有平台的依赖，生成真正的跨平台 JAR 文件。

## 故障排查

如果构建失败，请检查：
1. Gradle 构建配置是否正确
2. JDK 版本是否兼容
3. 依赖项是否可以正常下载

查看 [GitHub Actions](https://github.com/Yricky/abcde/actions) 页面的构建日志获取详细错误信息。
