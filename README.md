# TigerConnect Desktop App

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
* It will immediately launch the app after installation is complete.
* It will automatically download and install updates when they are available, if your organization allows this.

Windows Admin installer:
* It will install the TigerConnect Desktop App for all users on the system.
* It does not immediately launch the app after installation is complete.
* It will never download and install updates.

### Windows Commandline Options

The following commandline options may be provided to the Windows installers:

`/d="C:\Program Files"` or `/D="C:\Program Files"` or `/inst-dir="C:\Program Files"`
* Set the installation directory.
* Only absolute paths are supported.
* If the path contains spaces, it must be wrapped in double-quote characters.
* The path `\TigerConnect` will be added to the end of the supplied argument.
* Not supported as an uninstaller option.

`/run-at-startup=true`
* If `true` (the default setting) and the Admin installer is executed, this option controls whether to automatically run the TigerConnect app at system startup.
* If `true` (the default setting) and the Single-click installer is executed, this option controls whether to automatically run the TigerConnect app after the current user logs in.
* If `false`, the TigerConnect app will not be executed at system startup or login.
* Not supported as an uninstaller option.

`/s` or `/S` or `/silent`
* Do not show any prompts or UI during the installation process.
* When calling the uninstaller, use capitalized `/S`; the other `/s` and `/silent` variations are not supported.

`/?` or `/h` or `/help`
* Show this webpage.
* Not supported as an uninstaller option.

Example:

```sh
TigerConnect-Admin-Setup.exe /silent /run-at-startup=false
```

## Support

If you have any questions please reach out to the TigerConnect team at any time by visiting [https://tigerconnect.com/support/](https://tigerconnect.com/support/).
