# AGENTS.md

Guidance for coding agents working in this repository.

## Project Overview

Class2String is an IntelliJ IDEA plugin that generates SQL DDL and TypeScript types/interfaces from Java classes. The plugin id is `com.liuujun.class2dml`, while the marketplace/plugin name is `Class2String`.

## Repository Layout

- `build.gradle.kts`: Gradle build, IntelliJ Platform plugin configuration, publishing settings, and compatibility range.
- `settings.gradle.kts`: root project name.
- `src/main/java/com/liuujun/class2dml`: Java implementation for actions, settings UI, mappings, and utility classes.
- `src/main/kotlin/com/liuujun/class2dml`: Kotlin services, bundle helper, and UI dialog code.
- `src/main/resources/META-INF/plugin.xml`: plugin metadata, extension registrations, and action registrations.
- `src/main/resources/messages`: localization bundles. Keep English and `zh_CN` keys in sync.
- `doc`: README screenshots and GIFs.
- `CHANGELOG.md`: release notes consumed by the Gradle changelog plugin.

## Build And Verification

Use the Gradle wrapper from the repository root.

- Compile/check the project: `./gradlew build`
- Run the plugin in a sandbox IDE: `./gradlew runIde`
- Verify plugin packaging/signing-related checks where relevant: `./gradlew verifyPlugin`
- Build the distributable plugin artifact: `./gradlew buildPlugin`

The project targets JVM 17 and IntelliJ IDEA Ultimate `2026.1` through the IntelliJ Platform Gradle plugin. Avoid changing platform versions, plugin id, or compatibility bounds unless the task explicitly requires it.

## Development Notes

- Prefer existing packages and patterns under `com.liuujun.class2dml`.
- Actions are registered in `plugin.xml` and generally extend IntelliJ action APIs.
- User-visible text should go through `Class2dmlBundle` and both message bundle files.
- Keep generated SQL/TypeScript behavior consistent with the existing mapping classes and settings stored by `SettingStorage`.
- Be careful with IntelliJ PSI usage. Validate nullability and file/class shape before traversing PSI elements.
- Keep Java and Kotlin interop simple; do not introduce new frameworks for small changes.

## Release Notes

When making user-visible changes, add a short entry under `## [Unreleased]()` in `CHANGELOG.md`. The changelog plugin uses the latest entry for plugin change notes during `patchPluginXml`.

## Generated And Local Files

Do not edit generated or machine-local directories unless explicitly asked:

- `build/`
- `.gradle/`
- `.idea/`
- `.intellijPlatform/`

## Style

- Match the surrounding Java/Kotlin formatting.
- Keep comments sparse and useful.
- Use ASCII unless editing existing localized text or resources that already require non-ASCII.
- Keep changes narrowly scoped; avoid unrelated refactors.
