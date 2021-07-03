顶层的[win](configuration.md#Configuration-win)键包含一组选项，指示 electron-builder 应该如何构建 Windows 目标。这些选项适用于任何 Windows 目标。

<!-- do not edit. start of generated block -->

* <code id="WindowsConfiguration-target">target</code> = `nsis` String | [TargetConfiguration](/cli#targetconfiguration) - 目标打包类型：`nsis`列表、`nsis-web` (Web 安装程序)、`portable` (无需安装的 [便携式](/configuration/nsis#portable) 应用程序)、`appx`、`msi`、`squirrel`、`7z`、`zip`、`tar.xz`、`tar.lz`、`tar.gz`、`tar.bz2`、`dir`。 AppX 包只能在 Windows 10 上生成。

  如需使用 Squirrel.Windows ，请安装 `electron-builder-squirrel-windows` 依赖。

* <code id="WindowsConfiguration-icon">icon</code> = `build/icon.ico` String - 应用程序图标路径。

* <code id="WindowsConfiguration-legalTrademarks">legalTrademarks</code> String - 商标和注册商标。

---

* <code id="WindowsConfiguration-signingHashAlgorithms">signingHashAlgorithms</code> = `['sha1', 'sha256']` Array&lt;"sha1" | "sha256"&gt; - 使用的签名算法数组。AppX 总是使用`sha256`。
* <code id="WindowsConfiguration-sign">sign</code> String | (configuration: CustomWindowsSignTaskConfiguration) => Promise - 用于签署 Windows 可执行文件的自定义函数 (或文件或模块 ID 的路径)。
* <code id="WindowsConfiguration-certificateFile">certificateFile</code> String - 要签名的 *.pfx 证书路径。请仅在因为某些原因不能使用env环境变量 `CSC_LINK` (`WIN_CSC_LINK`) 时使用。请参阅 [代码签名](/code-signing) 。
* <code id="WindowsConfiguration-certificatePassword">certificatePassword</code> String - `certificateFile`中提供的证书的密码。请仅在因为某些原因不能使用env环境变量 `CSC_KEY_PASSWORD` (`WIN_CSC_KEY_PASSWORD`) 时使用。请参阅 [代码签名](/code-signing) 。
* <code id="WindowsConfiguration-certificateSubjectName">certificateSubjectName</code> String - 签名证书的主题名称。仅适用于 EV 代码签名且仅适用于 Windows ( 如果 [Parallels Desktop](https://www.parallels.com/products/desktop/) Windows 10 虚拟机退出，则 macOS 也可以适用) 。
* <code id="WindowsConfiguration-certificateSha1">certificateSha1</code> String - 签名证书的 SHA1 哈希值。当多个证书满足其余转换器指定的准则时，通常会指定 SHA1 哈希值。仅适用于 Windows (如果 [Parallels Desktop](https://www.parallels.com/products/desktop/) Windows 10 虚拟机退出，则 macOS 也可以适用).
* <code id="WindowsConfiguration-additionalCertificateFile">additionalCertificateFile</code> String - 要添加到签名块的附加证书文件的路径。
* <code id="WindowsConfiguration-rfc3161TimeStampServer">rfc3161TimeStampServer</code> = `http://timestamp.comodoca.com/rfc3161` String - RFC 3161 时间戳服务器的 URL。
* <code id="WindowsConfiguration-timeStampServer">timeStampServer</code> = `http://timestamp.digicert.com` String -  时间戳服务器的 URL。

---

* <code id="WindowsConfiguration-publisherName">publisherName</code> String | Array&lt;String&gt; - [发布者名称](https://github.com/electron-userland/electron-builder/issues/1187#issuecomment-278972073)，与您的代码签名证书完全相同。可以提供多个名称。默认为代码签名证书中的通用名称。
* <code id="WindowsConfiguration-verifyUpdateCodeSignature">verifyUpdateCodeSignature</code> = `true` Boolean -是否在安装前验证可用更新的签名。 [发布者名称](#publisherName) 将用于签名验证。
* <code id="WindowsConfiguration-requestedExecutionLevel">requestedExecutionLevel</code> = `asInvoker` "asInvoker" | "highestAvailable" | "requireAdministrator" - 应用请求执行的 [安全级别](https://msdn.microsoft.com/en-us/library/6ad1fshk.aspx#Anchor_9) 。不能为每个目标指定，且仅使用于 `win` 平台。
* <code id="WindowsConfiguration-signAndEditExecutable">signAndEditExecutable</code> = `true` Boolean - 是否对可执行文件进行签名并添加元数据。高级选项。
* <code id="WindowsConfiguration-signDlls">signDlls</code> = `false` Boolean - 是否对DLL文件进行签名。高级选项。参阅：https://github.com/electron-userland/electron-builder/issues/3101#issuecomment-404212384

<!-- end of generated block -->

---

{!includes/platform-specific-configuration-note.md!}

## 常见问题

#### 如何委托代码签名？

使用 [sign](#WindowsConfiguration-sign) 选项。另请参阅 [why sign.js is called 8 times](https://github.com/electron-userland/electron-builder/issues/3995).

```json
"win": {
  "sign": "./customSign.js"
}
```

项目根目录下的 `customSign.js` 文件：

```js
exports.default = async function(configuration) {
  // your custom code
}
```

#### 如何创建 Parallels Windows 10 虚拟机？

!!! 警告 "禁用 "Share Mac user folders with Windows""
    如果使用了 Parallels，则 [不能使用](https://github.com/electron-userland/electron-builder/issues/865#issuecomment-258105498) "Share Mac user folders with Windows" 功能，且不得从此类文件夹运行安装程序。

您不需要拥有Windows 10许可。提供免费 (90天后到期，但这不是问题，因为不需要额外设置)。

1. 打开 Parallels Desktop；
2. 文件 -> 新建；
3. 在 "Free Systems" 中选择 "Modern.IE"；
4. 继续，继续，接受软件许可协议；
5. 选择 "Microsoft Edge on Windows 10".
6. 后续的步骤是通用的，参见"步骤6：指定名称和位置"的 [使用 Parallels Desktop 在 Mac 上安装 Windows](http://kb.parallels.com/4729) 。

在 macOS 上构建AppX时会自动使用 Parallels Windows 10 虚拟机。甚至不需要启动虚拟机 — 它会在需要的时候自动启动，并在构建完成后自动中止。不需要指定虚拟机 — 它会自动检测 (第一个 Windows 10 虚拟机会被使用)。

#### 如何创建 VirtualBox Windows 10 虚拟机？

如果您没有使用 macOS 或者不想购买 [Parallels Desktop](https://www.parallels.com/products/desktop/)，您可以使用免费的 [VirtualBox](https://www.virtualbox.org/wiki/Downloads).

1. 打开 [Download virtual machines](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/).
2. 选择 "MSEdge on Win10 (x64) Stable".
3. 选择 "VirtualBox" 平台.
4. 下载。参见 [安装说明](https://az792536.vo.msecnd.net/vms/release_notes_license_terms_8_1_15.pdf).

您的虚拟机密码是 `Passw0rd!`.

electron-builder 目前不支持 VirtualBox，所以如果您想使用 VirtualBox 构建 AppX (或其它仅Windows支持的任务)，您需要在Windows上配置构建环境。