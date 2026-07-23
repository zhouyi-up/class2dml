# Repository Guidelines

## 项目结构与模块组织

Class2String 是 IntelliJ IDEA 插件，用于从 Java 类生成 SQL DDL 与 TypeScript 类型/接口。核心代码位于 `src/main/java/com/liuujun/class2dml` 与 `src/main/kotlin/com/liuujun/class2dml`。动作、映射和工具类主要在 Java 包中；服务、资源访问和部分 UI 对话框在 Kotlin 包中。

资源文件位于 `src/main/resources`：`META-INF/plugin.xml` 注册插件扩展与动作，`messages/` 存放英文与 `zh_CN` 本地化文案，修改用户可见文本时必须保持 key 同步。`doc/` 保存 README 使用的截图与 GIF。当前仓库未设置独立 `src/test` 目录；新增测试时应按 Gradle/JVM 常规结构放在 `src/test/java` 或 `src/test/kotlin`。

## 构建、测试与开发命令

从仓库根目录使用 Gradle Wrapper：

- `./gradlew build`：编译并执行常规检查。
- `./gradlew runIde`：在沙箱 IDE 中运行插件，适合手动验证动作与设置页。
- `./gradlew verifyPlugin`：执行插件兼容性与打包相关校验。
- `./gradlew buildPlugin`：生成可分发插件包。

项目使用 Gradle Wrapper 构建，当前面向 IntelliJ IDEA 2026.2（262.*）验证。IDEA 2026.2 依赖 Java 25 class 文件，本地构建应使用 JDK 25。

## 编码风格与命名约定

遵循现有 Java/Kotlin 风格和包结构，优先复用 `com.liuujun.class2dml` 下已有模式。动作类通常注册在 `plugin.xml` 并继承 IntelliJ Action API。涉及 PSI 遍历时先判断空值、文件类型和类结构，避免假设输入一定合法。

用户可见文案通过 `Class2dmlBundle` 获取，并同步维护 `Class2dmlBundle.properties` 与 `Class2dmlBundle_zh_CN.properties`。注释保持少量且有帮助，不为显而易见的代码添加解释。

## 测试与验证

优先使用 `./gradlew build` 做基础验证。涉及插件 UI、动作注册、设置存储或 PSI 行为时，同时使用 `./gradlew runIde` 手动验证。新增测试应贴近变更风险，测试命名清晰描述行为，例如 `SqlTypeMappingTest` 或 `TypeScriptInterfaceActionTest`。

## 提交与 Pull Request 规范

Git 历史中既有版本号式提交，也有中文说明。提交信息应简短说明变更目的，例如 `修复 TypeScript 类型映射` 或 `Update plugin compatibility metadata`。PR 应包含变更摘要、验证命令结果、相关 issue；涉及 UI 或生成结果变化时附截图、GIF 或示例输出。

## 发布说明与本地文件

用户可见变更需要在 `CHANGELOG.md` 的 `## [Unreleased]()` 下添加简短条目。不要编辑生成或本机目录，除非任务明确要求：`build/`、`.gradle/`、`.idea/`、`.intellijPlatform/`。
