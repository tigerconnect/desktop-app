# TigerConnect Desktop App

## Description

The TigerConnect Desktop App is nearly identical to the Web Messenger in function, but provides additional features
like notifications, icon badges, etc., and is more secure given there is no need to use a web browser. Additionally,
for those users that wish to have priority messaging with TigerConnect, using the Desktop App allows for uncluttered
access to TigerConnect in a standalone app.

## Requirements

**Hardware**
* The TigerConnect Desktop App installer is less than 100 MB and requires at least 750 MB of disk space for installation.

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

The TigerConnect Desktop App Admin Installer for Windows may be downloaded at the following location:

* [Windows - Admin installer](https://github.com/tigerconnect/desktop-app/releases/latest/download/TigerConnect-Admin-Setup.exe)

Other installation options:

* [Windows - Single-click installer](https://github.com/tigerconnect/desktop-app/releases/latest/download/TigerConnect-Setup.exe)
* [Mac OS](https://github.com/tigerconnect/desktop-app/releases/latest/download/TigerConnect.dmg)
* [Debian-compatible GNU/Linux](https://github.com/tigerconnect/desktop-app/releases/latest/download/TigerConnect-latest.deb)


## Installation

### Windows Installer Differences

Windows Single-click installer:
* Single user experience.
* It will install the TigerConnect Desktop App for the current user.
* It will not prompt for the installation location.
* It will immediately launch the app after installation is complete.
* It will automatically download and install updates when they are available, if your organization allows this.

Windows Admin installer:
* Multi user experience.
* For managed networks.
* It will install the TigerConnect Desktop App for all users on the system.
* It will prompt for the installation location and whether to run the app at login.
* It does not immediately launch the app after installation is complete.
* It will never download and install updates.
* It will work on Windows Terminal Server and Citrix Xenapp/desktop

### Windows Commandline Options

The following commandline options may be provided to the Windows installers:

`/d="C:\Program Files"` or `/D="C:\Program Files"` or `/inst-dir="C:\Program Files"`
* Set the installation directory.
* Only absolute paths are supported.
* If the path contains spaces, it must be wrapped in double-quote characters.
* The path `\TigerConnect` will be added to the end of the supplied argument if it is not present in the path argument.
* If omitted, the application will default to installing to "C:\Program Files\TigerConnect".

`/disable-sandbox`
* Disables the Chromium sandbox. This should be used with caution since sandboxing is a security feature, and should only be used at the direction of your TigerConnect support representative.
* This may be necessary if you are running our application on a network drive.
* Once installed, this setting can also be updated with `disableSandbox` in the configuration file described in [Advanced Topics](#advanced-topics).

`--force-run`
* Runs the application after installation is complete.
* This option has no effect on the one-click installer unless `/silent` is also passed, since the one-click installer will automatically run the application after installation is complete.
* This option cannot be used on the Admin installer unless `/silent` is also passed.

`--no-desktop-shortcut`
* Prevents the installer from creating a desktop shortcut for TigerConnect.

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

`/url="https://login.mysso.com/"` or `/URL="https://login.mysso.com/"`
* The URL feature is only needed when SSO is enabled, please contact your TigerConnect Sales representative for this premium feature.
* Set the URL the application will navigate to when opened.
* The URL must be wrapped in double-quote characters.
* Once installed, this setting can also be updated with `targetUrl` in the configuration file described in [Advanced Topics](#advanced-topics).
* If omitted, the application will default to opening "https://login.tigerconnect.com/".

`/use-custom-notifications`
* Use our custom notifications.
* This can be useful when the built-in ones do not work (e.g., with Citrix).
* Once installed, this setting can also be updated with `useCustomNotifications` in the configuration file described in [Advanced Topics](#advanced-topics).

`/s` or `/S` or `/silent`
* Do not show any prompts or UI during the installation process.
* Causes the app to not be executed automatically by the one-click installer after installation is complete. To allow the app to execute automatically anyway, use `--force-run` option in addition to this option.
* When calling the uninstaller, use capitalized `/S`; the other `/s` and `/silent` variations are not supported.

`/?` or `/h` or `/help`
* Show this webpage.


Example:

```sh
TigerConnect-Admin-Setup.exe /silent /run-at-login=false /url="https://login.tigerconnect.com/"
```

### Citrix Installation

Our default application runs into some restrictions when used with Citrix. In order to work around those issues, we recommend installing TigerConnect with at least the following commandline options.

```sh
TigerConnect-Admin-Setup.exe /disable-sandbox /use-custom-notifications
```

Many adminstrators also prefer to install our application with the minimum amount of dialogs and control when the application starts manually.

```sh
TigerConnect-Admin-Setup.exe /disable-sandbox /use-custom-notifications /silent /run-at-login=never
```
### Uninstall

The following command line switch is all that is needed to uninstall:

Example:

```
TigerConnect-Admin-Setup.exe /S  (must use a capital S)
```

## Application Commandline Options

The following commandline options may be provided to the Windows application executable:

`--enable-logging`

* This is a Chromium flag and will print Chrome's internal logging to the console.
* This can be useful when the application fails to open or when the DevTools cannot be opened.

`--disable-gpu`

* This is a Chromium flag and will disable GPU hardware acceleration.
* This can be useful when the application is running on a virtual environment where there is no GPU available.

Example:

```
TigerConnect.exe --enable-logging --disable-gpu
```

## Advanced Topics

**(Only needed when SSO is enabled, please contact your TigerConnect Sales representative for this premium feature)**

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

## License

The license for this application [may be viewed here](https://tigerconnect.github.io/desktop-app/license.html).

## Frequently Asked Questions (FAQs)

### Do I Need .NET or Java Installed?

No, our desktop application comes bundled with everything it needs to run.

### Why Can't I See Notifications?

Are you using Citrix? If so, you'll want to check out our [Citrix Installation section](#citrix-installation).

Otherwise, please go through the following checklist.

- Are notifications enabled in the TigerConnect application (User Profile -> Desktop App Settings)?
- Is the Windows system notifications enabled and is TigerConnect allowed to send notifications?
- Is Windows focus assist enabled and is TigerConnect in the priority list?

### Is There an MSI Version Available?

No, but you can either build one with free online tools or use the executable with a startup script in Group Policy to deploy. All the [switches](#windows-commandline-options) are built into the executable.
