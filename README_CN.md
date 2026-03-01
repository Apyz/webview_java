# Webview (Java 版)

[English](./README.md) | 中文版

这是 [webview project](https://github.com/webview/webview) 的 Java 移植版本。它使用 JNA 技术，并能根据你的当前系统自动提取所需的 dll/dylib/so 库文件。

<div align="center">
    <img alt="browser" src="demo.png" width="50%" />
    <br />
    <br />
</div>

## 本分支的改动
- 回退了部分二进制文件以修复 Windows 上的错误
- 获取地址: https://jitpack.io/#Osiris-Team/webview_java

## 本地工作区修复 (当前更新)
为了解决现代 Java 环境（特别是 **JDK 25**）中的编译和兼容性问题，我实施了以下改进：

1.  **移除 Lombok 依赖**：
    - 将所有 Lombok 注解（如 `@Getter`, `@Setter`, `@NonNull`, `@SneakyThrows` 等）替换为标准 Java 代码。
    - 这解决了在新版本 JDK 上由于 Lombok 未能及时跟进导致的“编译致命错误”，并且你不再需要安装 IDE 的 Lombok 插件。
2.  **修正模块版本号**：
    - 将 `pom.xml` 文件中所有的 `PLACEHOLDER` 版本字符串替换为具体版本（`1.0.0`）。
    - 确保了 Maven 和 IDE 能正确解析内部模块（`core`, `bridge` 等）的依赖关系。
3.  **提升 Java 11/25 兼容性**：
    - 重构了 `Webview.java` 中的构造函数，确保符合 Java 11 标准（防止在 `this()` 调用前出现逻辑语句）。
    - 显式添加了空指针检查和健壮的 `try-catch` 块。
4.  **验证构建流程**：
    - 项目现在可以通过标准 Maven 命令直接构建：`mvn clean compile`。

---

## 示例
[基础示例 (Example)](https://github.com/webview/webview_java/blob/main/core/src/test/java/com/example/webview_java/Example.java)  
[桥接示例 (Bridge Example)](https://github.com/webview/webview_java/blob/main/bridge/src/test/java/com/example/webview_java/BridgeExample.java)

## 支持的平台

<table width=300>
    <tr>
        <td align="right" width=100>
            Windows
        </td>
        <td align="left">
            x86, x86_64
        </td>
    </tr>
    <tr>
        <td align="right" width=100>
            macOS
        </td>
        <td align="left">
            aarch64, x86_64
        </td>
    </tr>
    <tr>
        <td align="right" width=100>
            Linux
        </td>
        <td align="left">
            x86, x86_64, arm, aarch64
        </td>
    </tr>
</table>

### Linux
原生支持 MUSL 和 GLibC。因此在 Debian, Arch, 和 Alpine 等发行版上应该都能正常工作。

### macOS
macOS 要求所有的 UI 代码必须在第一线程执行，这意味着启动 Java 时需要带上 `-XstartOnFirstThread` 参数。这也意味着 Webview AWT 助手将完全无法工作。

## 获取代码 (Maven/Gradle)

[![](https://jitpack.io/v/webview/webview_java.svg)](https://jitpack.io/#webview/webview_java)

将 `_VERSION` 替换为此仓库中的最新版本或提交号。如果你需要 Bridge 绑定，则需要同时引入 `core` 和 `bridge`。

<details>
  <summary>Maven</summary>
  
```xml
<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>

<dependency>
    <groupId>com.github.webview.webview_java</groupId>
    <artifactId>core</artifactId>
    <version>_VERSION</version>
</dependency>
```
</details>

<details>
<summary>Gradle</summary>

```gradle
allprojects {
  repositories {
    maven { url 'https://jitpack.io' }
  }
}

dependencies {
  implementation 'com.github.webview.webview_java:core:_VERSION'
}
```

</details>
