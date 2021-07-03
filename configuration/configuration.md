可以定义 electron-builder 的 [配置](#configuration)

* 在项目的 `package.json` 文件中的最顶层使用 `build` 键：

  ```json
  "build": {
    "appId": "com.example.app"
  }
  ```

* 或通过 `--config <path/to/yml-or-json5-or-toml-or-js>` 配置项。默认为 `electron-builder.yml`.

  ```yaml
  appId: "com.example.app"
  ```

   `json`、[json5](http://json5.org)、[toml](https://github.com/toml-lang/toml) 或 `js` (导出的配置或生成配置的函数) 格式均支持。

   !!! 注意
       如果您想使用 [toml](https://en.wikipedia.org/wiki/TOML)，请安装 `yarn add toml --dev`。

大部分配置项接受 `null` 值 — 例如，要明确设置 DMG 图标必须是操作系统的默认音量图标并且禁用默认设置 (即，使用应用程序图标作为 DMG 图标)，将 `dmg.icon` 设置为 `null`。

## 工件文件名模板

除了 [文件宏](../file-patterns.md#file-macros)，`${ext}` 宏也受支持。

## 来自文件的环境变量

当前目录下的 Env 文件 `electron-builder.env` ([示例](https://github.com/motdotla/dotenv-expand/blob/master/test/.env))。仅支持 CLI 使用。

## 如何阅读文档

* 可选属性的 `name` 使用常规字体，**`必备`** 属性使用加粗字体。
* 在属性名后指定类型：`Array<String> | String`。像这样的联合体表示您可以指定为字符串 (`**/*`)，或字符串数组 (`["**/*", "!foo.js"]`)。

## 配置

<!-- do not edit. start of generated block -->

* <code id="Configuration-appId">appId</code> = `com.electron.${name}` String - 应用程序 id。用作 MacOS 的 [CFBundleIdentifier](https://developer.apple.com/library/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html#//apple_ref/doc/uid/20001431-102070) ，或 Windows 的 [应用程序用户模型 ID](https://msdn.microsoft.com/en-us/library/windows/desktop/dd378459(v=vs.85).aspx) (仅限 NSIS 目标，不支持 Squirrel.Windows)。强烈建议显式设置ID。
* <code id="Configuration-productName">productName</code> String - 与 [name](#Metadata-name) 属性相似，但允许您为您的可执行文件指定一个包含空格和其他特殊字符在内的产品名称，空格和特殊字符在 [name](https://docs.npmjs.com/files/package.json#name) 属性中则不能使用。如果这个值不含非法字符 (括号、方括号、破折号等)，它将被用作安装目录 (除非用户使用<code>allowToChangeInstallationDirectory</code>)覆盖它。如果包含非法字符，安装目录名称会默认返回到 [name](#Metadata-name) 属性。
* <code id="Configuration-copyright">copyright</code> = `Copyright © year ${author}` String - 可读的版权信息。

---

* <code id="Configuration-directories">directories</code><a name="MetadataDirectories"></a>

  * <code id="MetadataDirectories-buildResources">buildResources</code> = `build` String - 构建资源的路径。

    请注意 — 构建资源不会被打包到程序中。如果您需要使用某些文件，如托盘图标，请显式地包含需要的文件：`"files": ["**/*", "build/icon.*"]`

  * <code id="MetadataDirectories-output">output</code> = `dist` String - 输出目录。支持 [文件宏](/file-patterns#file-macros) 。

  * <code id="MetadataDirectories-app">app</code> String - 应用程序目录 (包含应用程序的 package.json 文件)，默认为 `app`、`www` 或工作目录。

---

* <code id="Configuration-mac">mac</code> [MacConfiguration](mac) - 与如何构建 macOS 目标相关的配置项。
* <code id="Configuration-mas">mas</code> [MasConfiguration](mas) - MAS（Mac 应用程序商店）配置项。
* <code id="Configuration-dmg">dmg</code> [DmgOptions](dmg) - macOS DMG 配置项。
* <code id="Configuration-pkg">pkg</code> [PkgOptions](pkg) - macOS PKG 配置项。

---

* <code id="Configuration-win">win</code> [WindowsConfiguration](win) - 与如何构建 Windows 目标相关的配置项。

* <code id="Configuration-nsis">nsis</code> [NsisOptions](nsis)

* <code id="Configuration-nsisWeb">nsisWeb</code><a name="NsisWebOptions"></a> - Web 安装程序项。
  继承 [NsisOptions](nsis) 项.

  * <code id="NsisWebOptions-appPackageUrl">appPackageUrl</code> String - 应用程序包下载 URL 。可选 — 默认根据发布配置生成。

    类似 `https://example.com/download/latest` 的 URL 允许 web 安装程序独立于版本 (安装程序会下载最新的应用程序包)。请注意 — 该项必须是 [完整的 URL](https://github.com/electron-userland/electron-builder/issues/1810#issuecomment-317650878)。

    自定义 `X-Arch` http 头设置为 `32` 或 `64`。

  * <code id="NsisWebOptions-artifactName">artifactName</code> String - [工件文件名模板](/configuration/configuration#artifact-file-name-template)。 默认为 `${productName} Web Setup ${version}.${ext}`.

* <code id="Configuration-portable">portable</code><a name="PortableOptions"></a> - 便携式目标配置项。

  * <code id="PortableOptions-requestExecutionLevel">requestExecutionLevel</code> = `user` "user" | "highest" | "admin" - Windows 的 [请求执行级别](http://nsis.sourceforge.net/Reference/RequestExecutionLevel) 。

  * <code id="PortableOptions-unpackDirName">unpackDirName</code> String - [TEMP](https://www.askvg.com/where-does-windows-store-temporary-files-and-how-to-change-temp-folder-location/) 目录中的解包目录名称。

    默认为构建的 [uuid](https://github.com/segmentio/ksuid) (每次构建可执行文件时更改)。

* <code id="Configuration-appx">appx</code> [AppXOptions](appx)

* <code id="Configuration-squirrelWindows">squirrelWindows</code> [SquirrelWindowsOptions](squirrel-windows.md)

---

* <code id="Configuration-linux">linux</code> [LinuxConfiguration](linux) - 与如何构建 Linux 目标相关的配置项。
* <code id="Configuration-deb">deb</code> [DebOptions](/configuration/linux#de) - Debian 软件包配置项。
* <code id="Configuration-snap">snap</code> [SnapOptions](snap) - Snap 配置项。
* <code id="Configuration-appImage">appImage</code> [AppImageOptions](/configuration/linux#appimageoptions) - AppImage 配置项。
* <code id="Configuration-pacman">pacman</code> [LinuxTargetSpecificOptions](/configuration/linux#LinuxTargetSpecificOptions)
* <code id="Configuration-rpm">rpm</code> [LinuxTargetSpecificOptions](/configuration/linux#LinuxTargetSpecificOptions)
* <code id="Configuration-freebsd">freebsd</code> [LinuxTargetSpecificOptions](/configuration/linux#LinuxTargetSpecificOptions)
* <code id="Configuration-p5p">p5p</code> [LinuxTargetSpecificOptions](/configuration/linux#LinuxTargetSpecificOptions)
* <code id="Configuration-apk">apk</code> [LinuxTargetSpecificOptions](/configuration/linux#LinuxTargetSpecificOptions)

---

* <code id="Configuration-buildDependenciesFromSource">buildDependenciesFromSource</code> = `false` Boolean - 是否从源文件生成应用程序本地依赖。
* <code id="Configuration-nodeGypRebuild">nodeGypRebuild</code> = `false` Boolean - 是否在打包应用程序前执行 `node-gyp rebuild` 。

  不要 [使用](https://github.com/electron-userland/electron-builder/issues/683#issuecomment-241214075) [npm](http://electron.atom.io/docs/tutorial/using-native-node-modules/#using-npm) (或 `.npmrc`) 来配置 electron 头文件。 使用 `electron-builder node-gyp-rebuild` 代替。

* <code id="Configuration-npmArgs">npmArgs</code> Array&lt;String&gt; | String - 在安装应用程序本地依赖时使用的其他命令行参数。

* <code id="Configuration-npmRebuild">npmRebuild</code> = `true` Boolean - 是否在打包应用前 [重建](https://docs.npmjs.com/cli/rebuild) 本地依赖。

---

* <code id="Configuration-buildVersion">buildVersion</code> String - 构建版本。映射到macOS的 `CFBundleVersion`，或 Windows 的 `FileVersion` 元数据属性。 默认为 `version`。如果定义了 `TRAVIS_BUILD_NUMBER`、`APPVEYOR_BUILD_NUMBER`、`CIRCLE_BUILD_NUM`、`BUILD_NUMBER`、`bamboo.buildNumber`、`CI_PIPELINE_IID` 等环境，它将被用为构建版本 (`version.build_number`).

* <code id="Configuration-electronCompile">electronCompile</code> Boolean - 是否使用 [electron-compile](http://github.com/electron/electron-compile) 编译应用程序。`electron-compile` 如果在运行依赖中则默认为 `true`，如果在开发依赖中或没有指定则默认为`false`。

* <code id="Configuration-electronDist">electronDist</code> String - 自定义Electron 构建的路径 (如：`~/electron/out/R`).

* <code id="Configuration-electronDownload">electronDownload</code><a name="ElectronDownloadOptions"></a> - [electron-download](https://github.com/electron-userland/electron-download#usage) 配置项。

  * <code id="ElectronDownloadOptions-version">version</code> String
  * <code id="ElectronDownloadOptions-cache">cache</code> String - [缓存位置](https://github.com/electron-userland/electron-download#cache-location).
  * <code id="ElectronDownloadOptions-mirror">mirror</code> String - 镜像
  * <code id="ElectronDownloadOptions-strictSSL">strictSSL</code> Boolean
  * <code id="ElectronDownloadOptions-isVerifyChecksum">isVerifyChecksum</code> Boolean
  * <code id="ElectronDownloadOptions-platform">platform</code> "darwin" | "linux" | "win32" | "mas"
  * <code id="ElectronDownloadOptions-arch">arch</code> String

* <code id="Configuration-electronVersion">electronVersion</code> String - 您要打包的 electron 版本。默认使用 `electron`、`electron-prebuilt`、`electron-prebuilt-compile` 依赖的版本。

* <code id="Configuration-extends">extends</code> String - 内置配置预设的名称或配置文件的路径 (相对于项目目录)。目前仅支持 `react-cra`。

  如果 `react-scripts` 在应用程序依赖中，`react-cra` 会被自动设置。设置为 `null` 禁用自动检测。

* <code id="Configuration-extraMetadata">extraMetadata</code> any - 将属性注入到 `package.json`。

* <code id="Configuration-readonly">readonly</code> = `false` Boolean - 应用程序未签名时是否失败 (在代码签名配置不正确时防止未签名的应用程序)。

* <code id="Configuration-nodeVersion">nodeVersion</code> String - *仅基于libui的框架* 您要打包的NodeJS版本。您可以设置为 `current` 来使用您正在运行的 Node.js 版本。

* <code id="Configuration-launchUiVersion">launchUiVersion</code> Boolean | String - *仅基于libui的框架* 您正在打包的 LaunchUI 版本。仅 Windows 可用。默认为适用于所用框架版本的版本。

* <code id="Configuration-framework">framework</code> String - 框架名。 `electron`、`proton-native`、`libui` 中的一个，且默认为 `electron`。

---

* <code id="Configuration-afterPack">afterPack</code> - [打包后运行](#afterpack) (但在打包进可移植格式和签名之前)的函数(或文件、模块id的路径)。

* <code id="Configuration-afterSign">afterSign</code> - [打包和签名后](#aftersign) 运行的函数(或文件、模块id的路径)(但在打包进可移植格式之前).

* <code id="Configuration-artifactBuildStarted">artifactBuildStarted</code> module:app-builder-lib/out/configuration.__type | String - 工件构建开始时运行的函数(或文件、模块 ID 的路径)。

* <code id="Configuration-artifactBuildCompleted">artifactBuildCompleted</code> module:app-builder-lib/out/configuration.__type | String - 工件构建完成时运行的函数（或文件、模块 ID 的路径）。

* <code id="Configuration-afterAllArtifactBuild">afterAllArtifactBuild</code> - [所有工件构建后](#afterAllArtifactBuild) 运行的函数（或文件、模块 ID 的路径）。

* <code id="Configuration-onNodeModuleFile">onNodeModuleFile</code> - [在每个node模块](#onnodemodulefile) 文件上运行的函数（或文件、模块 ID 的路径）。

* <code id="Configuration-beforeBuild">beforeBuild</code> (context: BeforeBuildContext) => Promise | null - 在运行依赖安装后或重建后运行的函数（或文件、模块 ID 的路径）。在 `npmRebuild` 为 `true` 时有效。设置为 `false` 会跳过运行依赖安装和重建。

  如果提供了beforeBuild 但缺失 `node_modules`，则不会调用生产依赖项检查。

---

* <code id="Configuration-remoteBuild">remoteBuild</code> = `true` Boolean -  如果当前操作系统不支持目标，是否使用 Electron Build 服务进行构建。
* <code id="Configuration-includePdb">includePdb</code> = `false` Boolean - 是否包含 PDB 文件。
* <code id="Configuration-removePackageScripts">removePackageScripts</code> = `true` Boolean - 是否从 `package.json` 文件移除 `scripts` 字段。

<!-- end of generated block -->

---

### 每个平台可重写的配置项

如果需要，还可以为每个平台(最顶层键为 [mac](mac.md)、[linux](linux.md) 或 [win](win.md))设置以下选项。

{!generated/PlatformSpecificBuildOptions.md!}

## Metadata

一些应该在 `package.json` 中定义的标准字段。

{!generated/Metadata.md!}

## Proton Native

要打包 [Proton Native](https://proton-native.js.org/) 应用，设置 `protonNodeVersion` 项为 `current` ，或您要打包的特定 NodeJS 版本。
目前仅 macOS 和 Linux 支持。

## 构建版本管理

macOS 的 `CFBundleVersion` 和 Windows 的 `FileVersion` 在 CI 服务器上会被自动设置为 `version.build_number` (支持 Travis、AppVeyor、CircleCI 和 Bamboo )。

{!includes/hooks.md!}