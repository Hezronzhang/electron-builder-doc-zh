electron-builder [![npm version](https://img.shields.io/npm/v/electron-builder.svg?label=latest)](https://yarn.pm/electron-builder) [![downloads per month](https://img.shields.io/npm/dm/electron-builder.svg)](https://yarn.pm/electron-builder) [![donate](https://img.shields.io/badge/donate-donorbox-green.svg)](https://www.electron.build/donate) [![project chat](https://img.shields.io/badge/chat-on_zulip-brightgreen.svg)](https://electron-builder.zulipchat.com)
***
electron-builder是一个完整的解决方案，用于打包和构建适用于 macOS、Windows 和 Linux 的准备分发 Electron 应用程序，具有开箱即用的“自动更新”支持。
* NPM包管理：
  * [本机应用程序依赖项](https://electron.atom.io/docs/tutorial/using-native-node-modules/) 编译 (包括 [Yarn](http://yarnpkg.com/) 支持)。
  * 未包含开发依赖项。您不需要明确地忽略它们。
  * 支持 [两个 package.json 结构](tutorials/two-package-structure.md) ，但即使有本地生产依赖，也不是强制要求使用它。
* CI服务器或开发机上的 [代码签名](code-signing.md)。
* [自动更新](auto-update.md) 就绪的程序打包。
* 多种目标格式：
  * 所有平台： `7z`、`zip`、`tar.xz`、`tar.lz`、`tar.gz`、`tar.bz2`、`dir` (解压目录)。
  * [macOS](configuration/mac.md#MacConfiguration-target)：`dmg`、`pkg`、`mas`、`mas-dev`。
  * [Linux](configuration/linux.md#LinuxConfiguration-target): [AppImage](http://appimage.org)、[snap](http://snapcraft.io)、debian package (`deb`)、`rpm`、`freebsd`、`pacman`、`p5p`、`apk`。
  * [Windows](configuration/win.md#WindowsConfiguration-target): `nsis` (安装程序)、`nsis-web` (Web 安装程序)、`portable` (无需安装的便携式程序)、AppX (Windows 应用商店)、Squirrel.Windows.
* [发布产品](configuration/publish.md) 到 GitHub Releases、Amazon S3、DigitalOcean Spaces 或 Bintray.
* 高级打包：
  * 打包成可发布的格式 [打包好的程序](#pack-only-in-a-distributable-format).
  * 拆分 [打包步骤](https://github.com/electron-userland/electron-builder/issues/1102#issuecomment-271845854).
  * 并行构建和发布，使用 CI 服务器上的硬链接来减少 IO 和磁盘空间使用。
  * [electron-compile](https://github.com/electron/electron-compile) 支持 （在构建时即时编译发布时间）。
* 用于在任何平台上为 Linux 或 Windows 构建 Electron 程序的 [Docker](multi-platform-build.md#docker) 镜像。
* [Proton Native](https://proton-native.js.org/) 支持.
* 自动按需下载所有必需的工具文件 (例如对 Windows 应用程序进行代码签名，制作 AppX)，无需设置。