# Changes in this fork
[English](./README.md) | [中文版](./README_CN.md)

- Reverted some binaries to fix bug on windows
- Get it from here: https://jitpack.io/#Osiris-Team/webview_java

## Fixes in this Workspace (Local Update)
To resolve compilation and compatibility issues in modern Java environments (specifically **JDK 25**), the following changes were implemented:

1.  **Removed Lombok Dependency**: 
    - Replaced all Lombok annotations (`@Getter`, `@Setter`, `@NonNull`, `@SneakyThrows`, etc.) with standard Java code.
    - This eliminates the need for the Lombok IDE plugin and fixes the "Fatal error compiling" issues seen on newer JDKs where Lombok hasn't yet caught up.
2.  **Corrected Module Versioning**:
    - Replaced all `PLACEHOLDER` version strings in `pom.xml` files with a concrete version (`1.0.0`). 
    - This allows Maven and IDEs to correctly resolve internal module dependencies (`core`, `bridge`, etc.).
3.  **Improved Java 11/25 Compatibility**:
    - Refactored constructors in `Webview.java` to ensure compliance with Java 11 standards (preventing statements before `this()` calls).
    - Added explicit null checks and robust `try-catch` blocks to replace previous annotation-driven logic.
4.  **Verified Build Process**:
    - The project now builds successfully using standard Maven commands: `mvn clean compile`.

# Webview

The Java port of the [webview project](https://github.com/webview/webview). It uses JNA and auto-extracts the required dll/dylib/so libraries for your current system.

<div align="center">
    <img alt="browser" src="demo.png" width="50%" />
    <br />
    <br />
</div>

## Examples

[Example](https://github.com/webview/webview_java/blob/main/core/src/test/java/com/example/webview_java/Example.java)  
[Bridge Example](https://github.com/webview/webview_java/blob/main/bridge/src/test/java/com/example/webview_java/BridgeExample.java)

## Supported Platforms

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
Both MUSL and GLibC are supported out of the box. So it should work fine under distros like Debian, Arch, and Alpine.

### macOS

macOS requires that all UI code be executed from the first thread, which means you will need to launch Java with `-XstartOnFirstThread`. This also means that the Webview AWT helper will NOT work at all.

## Getting the code

[![](https://jitpack.io/v/webview/webview_java.svg)](https://jitpack.io/#webview/webview_java)

Replace `_VERSION` with the latest version or commit in this repo. If you want the Bridge bindings you'll need both `core` and `bridge`.

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

<details>
  <summary>SBT</summary>

```sbt
resolvers += "jitpack" at "https://jitpack.io"

libraryDependencies += "com.github.webview.webview_java" % "core" % "\_VERSION"
```

</details>

<details>
<summary>Leiningen</summary>

```lein
:repositories [["jitpack" "https://jitpack.io"]]

:dependencies [[com.github.webview.webview_java/core "_VERSION"]]
```

</details>
