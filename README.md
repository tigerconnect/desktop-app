# TigerConnect Desktop App

## Description

The TigerConnect Desktop App is nearly identical to the Web Messenger in function, but provides additional features
like notifications, icon badges, etc., and is more secure given there is no need to use a web browser. Additionally,
for those users that wish to have priority messaging with TigerConnect, using the Desktop App allows for uncluttered
access to TigerConnect in a standalone app.

## Requirements

**Desktop App for Windows**
* Windows 7 (32/64-bit)
* Windows 8/8.1 (32/64-bit)
* Windows 10 (32/64-bit)

**Desktop App for Mac**
* OS X 10.10 (Yosemite) and newer (64-bit only)

**Desktop App for Linux**
* Debian 8 and newer
* Ubuntu 12.04 and newer

## Download

The TigerConnect Desktop App may be downloaded at the following locations:

* [Windows - Single-click installer](https://github.com/tigerconnect/desktop-app/releases/latest/download/TigerConnect-Setup.exe)
* [Mac OS](https://github.com/tigerconnect/desktop-app/releases/latest/download/TigerConnect.dmg)
* [Debian-compatible GNU/Linux](https://github.com/tigerconnect/desktop-app/releases/latest/download/TigerConnect-latest.deb)

Other installation options:

* [Windows - Admin installer](https://github.com/tigerconnect/desktop-app/releases/latest/download/TigerConnect-Admin-Setup.exe)

## Installation

### Windows Installer Differences

Windows Single-click installer:
* It will install the TigerConnect Desktop App for the current user.
* It will not prompt for the installation location.
* It will immediately launch the app after installation is complete.
* It will automatically download and install updates when they are available, if your organization allows this.

Windows Admin installer:
* It will install the TigerConnect Desktop App for all users on the system.
* It will prompt for the installation location and whether to run the app at login.
* It does not immediately launch the app after installation is complete.
* It will never download and install updates.

### Windows Commandline Options

The following commandline options may be provided to the Windows installers:

`/d="C:\Program Files"` or `/D="C:\Program Files"` or `/inst-dir="C:\Program Files"`
* Set the installation directory.
* Only absolute paths are supported.
* If the path contains spaces, it must be wrapped in double-quote characters.
* The path `\TigerConnect` will be added to the end of the supplied argument if it is not present in the path argument.
* Not supported as an uninstaller option.

`/disable-sandbox`
* Disables the Chromium sandbox. This should be used with caution since sandboxing is a security feature, and should only be used at the direction of your TigerConnect support representative.
* This may be necessary if you are running our application on a network drive.
* Once installed, this setting can also be updated with `disableSandbox` in the configuration file described in [Advanced Topics](#advanced-topics).
* Not supported as an uninstaller option.

`/run-at-login=true`
* If `true` (the default setting for the Single-Click installer):
  * The TigerConnect app will be executed after the current user logs in.
  * Not supported by the Admin installer.
* If `false` (the default setting for the Admin installer):
  * The TigerConnect app will not be executed when the current user logs in.
  * Other users on the system, after they launch TigerConnect at least once, will have run-at-login enabled by default.
* If `never` (only supported by the Admin installer):
  * The TigerConnect app will not be executed when the current user logs in.
  * Other users on the system, after they launch TigerConnect at least once, will have run-at-login disabled by default.
  * Not supported by the Single-Click installer.
* Not supported as an uninstaller option.

`/url="https://login.tigerconnect.com/"` or `/URL="https://login.tigerconnect.com/"`
* Set the URL the application will navigate to when opened. 
* The URL must be wrapped in double-quote characters.
* Once installed, this setting can also be updated with `targetUrl` in the configuration file described in [Advanced Topics](#advanced-topics).
* If omitted, the application will default to opening "https://login.tigerconnect.com/".
* Not supported as an uninstaller option.

`/s` or `/S` or `/silent`
* Do not show any prompts or UI during the installation process.
* When calling the uninstaller, use capitalized `/S`; the other `/s` and `/silent` variations are not supported.

`/?` or `/h` or `/help`
* Show this webpage.
* Not supported as an uninstaller option.

Example:

```sh
TigerConnect-Admin-Setup.exe /silent /run-at-login=false /url="https://login.tigerconnect.com/"
```

## Application Commandline Options

The following commandline options may be provided to the Windows application executable:

`--enable-logging`

* This is a Chromium flag and will print Chrome's internal logging to the console.
* This can be useful when the application fails to open or when the DevTools cannot be opened.

Example:

```
TigerConnect.exe --enable-logging
```

## Advanced Topics

### System Configuration File

As an advanced feature, a configuration file named `config.yaml` is available in the following locations after installing the app on Windows or running the app at least once. Settings here will be applied to every user on the system.

* Windows: `%PROGRAMDATA%\TigerConnect\config.yaml`; `%PROGRAMDATA%` is typically a value like `C:\ProgramData`
* Mac: `/Library/Application Support/TigerConnect/config.yaml`
* Linux: `/opt/TigerConnect/config.yaml`

It's not recommended to modify this file except at the behest of your TigerConnect support representative.

### User Configuration File

As an advanced feature, a user-specific configuration file named `config.yaml` is available in the following locations after installing the app on Windows or running the app at least once.

* Windows: `%APPDATA%\TigerConnect\config.yaml`; `%APPDATA%` is typically a value like `C:\Users\MyUser\AppData\Roaming`
* Mac: `~/Library/Application Support/TigerConnect/config.yaml`
* Linux: `~/.config/TigerConnect/config.yaml`

It's not recommended to modify this file except at the behest of your TigerConnect support representative.

## Support

If you have any questions please reach out to the TigerConnect team at any time by visiting [https://tigerconnect.com/support/](https://tigerconnect.com/support/).
