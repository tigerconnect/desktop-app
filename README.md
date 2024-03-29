# TigerConnect Desktop App

  * [Description](#description)
  * [Requirements](#requirements)
  * [Download](#download)
  * [Installation](#installation)
    + [Windows Installer Differences](#windows-installer-differences)
    + [Windows Commandline Options](#windows-commandline-options)
    + [Citrix Installation](#citrix-installation)
    + [Imprivata Installation](#imprivata-installation)
    + [Uninstall](#uninstall)
    + [Upgrade](#upgrade)
  * [Application Commandline Options](#application-commandline-options)
  * [Advanced Topics](#advanced-topics)
    + [System Configuration File](#system-configuration-file)
    + [User Configuration File](#user-configuration-file)
  * [Support](#support)
  * [License](#license)
  * [Frequently Asked Questions (FAQs)](#frequently-asked-questions-faqs)
    + [Do I Need .NET or Java Installed?](#do-i-need-net-or-java-installed)
    + [Why Can't I See Notifications?](#why-cant-i-see-notifications)
    + [Is There an MSI Version Available?](#is-there-an-msi-version-available)
    + [Why Isn't Integrated Windows Authentication SSO Working?](#why-isnt-integrated-windows-authentication-sso-working)

## Description

The TigerConnect Desktop App is nearly identical to the Web Messenger in function, but provides
additional features like notifications, icon badges, etc., and is more secure given there is no need
to use a web browser. Additionally, for those users that wish to have priority messaging with
TigerConnect, using the Desktop App allows for uncluttered access to TigerConnect in a standalone app.

## Requirements

**Hardware**
* The TigerConnect Desktop App installer is less than 100 MB and requires at least 750 MB of disk space for installation.

**Desktop App for Windows**
* Windows 7 (32/64-bit)
* Windows 8/8.1 (32/64-bit)
* Windows 10 (32/64-bit)
* Windows 11 (64-bit)

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

`/ntlm-domains="*.adomain.com, *.anotherdomain.com"`
* A comma-separated list of servers for which Integrated Windows Authentication is enabled. HTTP NTLM and Negotiate (Kerberos) authentication will be tried.
* Any domain listed will be considered for Integrated Windows Authentication.
* Enabling this option will have the additional effect of changing the way some Microsoft websites fingerprint the app, to ensure that SSO is correctly offered on Azure and other SAML landing pages (requires TigerConnect Desktop App 5.4.2 or later).

`/run-at-login=true`
* If `true` (the default setting for the Single-Click installer):
  * The TigerConnect app will be executed after the current user logs in.
  * Not supported by the Admin installer.
  * This has the effect of setting `hasInstalledAutoRun: false` (or removing the `hasInstalledAutoRun` setting) in the user-level configuration file, which can also be adjusted by editing that file as described in [Advanced Topics](#advanced-topics).
* If `false` (the default setting for the Admin installer):
  * The TigerConnect app will not be executed when the current user logs in.
  * Other users on the system, after they launch TigerConnect at least once, will have run-at-login enabled by default.
  * This has the effect of setting `hasInstalledAutoRun: true` (or removing the `hasInstalledAutoRun` setting) in the appropriate configuration file, which can also be adjusted by editing that file as described in [Advanced Topics](#advanced-topics).
* If `never` (only supported by the Admin installer):
  * The TigerConnect app will not be executed when the current user logs in.
  * Other users on the system, after they launch TigerConnect at least once, will have run-at-login disabled by default.
  * Not supported by the Single-Click installer.
  * This has the effect of setting `hasInstalledAutoRun: true` (or removing the `hasInstalledAutoRun` setting) in the system-level configuration file, which can also be adjusted by editing that file as described in [Advanced Topics](#advanced-topics).
* If multiple TigerConnect accounts are shared by the same Windows account, and Imprivata is used to automatically launch the TigerConnect app and fill credentials, it is recommended to provide `/run-at-login=false` as an installer option.
* Note: The installer will not try to directly add or remove the TigerConnect app from the Windows startup items.

`/show-native-ext-login`
* Displays a native login prompt for Basic HTTP authentication requests.
* Once installed, this setting can also be updated with `showNativeExtLogin` in the configuration file described in [Advanced Topics](#advanced-topics).

`/show-native-int-login-username`
* Displays a native login prompt for TigerConnect credentials (username only).
* If a TigerConnect password should be entered, please use the `show-native-int-login-username-password` commandline option instead.
* Once installed, this setting can also be updated with `showNativeIntLoginUsername` in the configuration file described in [Advanced Topics](#advanced-topics).

`/show-native-int-login-username-password`
* Displays a native login prompt for TigerConnect credentials (username and password).
* If only a TigerConnect username should be entered, please use the `show-native-int-login-username` commandline option instead.
* Once installed, this setting can also be updated with `showNativeIntLoginUsernamePassword` in the configuration file described in [Advanced Topics](#advanced-topics).

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

### Imprivata Installation

Our default application cannot be profiled with Imprivata. In order to work around that issue, we recommend installing TigerConnect with at least the following commandline options if users will be using an external authentication service that utilizes Basic HTTP authentication.

```sh
TigerConnect-Admin-Setup.exe /show-native-int-login-username /show-native-ext-login
```

If users will have TigerConnect-specific credentials (a username and password for our application), please use the following commandline option instead.

```sh
TigerConnect-Admin-Setup.exe /show-native-int-login-username-password
```

### Uninstall

After installation, an uninstallation executable called `Uninstall TigerConnect.exe` can be located in the installation directory (`C:/Program Files/TigerConnect` by default).

Running this executable will uninstall the TigerConnect Desktop App. You can provide the `/S` commandline option (must use a capital "S") to not show any prompts or UI during the uninstallation process.

Example for Admin installation:

```
"Uninstall TigerConnect.exe" /S
```

Example for Single-click installation (make sure to run this as the user who installed TigerConnect Desktop App):

```
"Uninstall TigerConnect.exe" /currentuser /S
```

Continue reading the `Upgrade` section for an example of how to locate Single-click installations to clean up before running the Admin installer.

### Upgrade

The following steps may be used to upgrade TigerConnect Desktop App:

* Download the installer for the new version that corresponds to your installation type (Admin or Single-click).
* Run the installer.

TigerConnect Desktop App is currently not able to remove a Single-click installation while using the Admin installer, since the Single-click installer is associated with a single user rather than the entire system. This may result in two app icons on the desktop, and two entries in the "Apps and Features" section of Control Panel.

To recover from this situation, it is recommended to uninstall the Single-click version manually as the user who originally installed it. Such Single-click installs (for version 5.x or higher) can be detected by:

* Open Registry Editor and search for `Uninstall TigerConnect.exe`
* There should be a match in `Computer\HKEY_USERS\...\CurrentVersion\Uninstall\...` for a key named `QuietUninstallString`
* Double click on the key, copy the "Value data" field.
* Paste that command into a Terminal session that is running as the user who the installation belongs to (which can be determined from the path to the executable).
* Execute that command to uninstall the Single-click variant of Desktop App.
* If multiple people may be using the machine, continue searching Registry Editor for more matches in the `HKEY_USERS` namespace.

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
* Mac (Standalone version): `/Library/Application Support/TigerConnect/config.yaml`
* Linux: `/opt/TigerConnect/config.yaml`

It's not recommended to modify this file except at the behest of your TigerConnect support representative.

Note that the Mac App Store version does not have a system configuration file.

### User Configuration File

As an advanced feature, a user-specific configuration file named `config.yaml` is available in the following locations after installing the app on Windows or running the app at least once.

* Windows: `%APPDATA%\TigerConnect\config.yaml`; `%APPDATA%` is typically a value like `C:\Users\MyUser\AppData\Roaming`
* Mac (Standalone version): `/Users/<user>/Library/Application Support/TigerConnect/config.yaml`
* Mac (App Store version): `/Users/<user>/Library/Containers/com.tigerconnect.macos/Data/Library/Application Support/TigerConnect/config.yaml`
* Linux: `~/.config/TigerConnect/config.yaml`

It's not recommended to modify this file except at the behest of your TigerConnect support representative.

Note that on the Mac App Store version, when editing `config.yaml` you may be prompted by OS X about allowing your editor access to other apps, and that has to be approved in order for the edits to succeed.

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

* Are notifications enabled in the TigerConnect application (User Profile -> Desktop App Settings)?
* Is the Windows system notifications enabled and is TigerConnect allowed to send notifications?
* Is Windows focus assist enabled and is TigerConnect in the priority list?

### Is There an MSI Version Available?

No, but you can either build one with free online tools or use the executable with a startup script in Group Policy to deploy. All the [switches](#windows-commandline-options) are built into the executable.

### Why Isn't Integrated Windows Authentication SSO Working?

You may need to try the following steps:

* Is the `ntlmDomains` option set? That option may need to be provided so that certain SAML providers fingerprint TigerConnect Desktop App correctly and allow SSO to be offered. One such case is Azure.
* Is the `targetUrl` option set? It may need to be either removed or (equivalently) returned to the default value of `"https://login.tigerconnect.com/app/messenger"` in order for the desired SSO flow to be triggered.
* When you go to the View menu -> "Toggle Developer Tools", go to Network tab and check "Preserve log", go to View menu -> "Reload", continue the login process, and look through some of the network requests with `/ssoprobe` or `/wia` in them, are they successful with a `200` status? If not, it may be necessary to compare with using the [TigerConnect Messenger website](https://login.tigerconnect.com/app/messenger) in Chrome or Edge, and/or reach out to [TigerConnect Professional Support](https://tigerconnect.com/support/) to help diagnose.
