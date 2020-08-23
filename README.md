# TigerConnect Desktop App

## Download

The TigerConnect Desktop App may be downloaded at the following locations:

* [Windows - Single-click installer](https://github.com/tigerconnect/desktop-app/releases/latest/download/TigerConnect-Setup.exe)
* [Windows - Admin installer](https://github.com/tigerconnect/desktop-app/releases/latest/download/TigerConnect-Admin-Setup.exe)
* [Mac OS](https://github.com/tigerconnect/desktop-app/releases/latest/download/TigerConnect.dmg)
* [Debian-compatible GNU/Linux](https://github.com/tigerconnect/desktop-app/releases/latest/download/TigerConnect-latest.deb)

## Installation

The following commandline arguments may be provided to the Windows installers:

`/D="C:\Program Files"`
* Set the installation directory.
* Only absolute paths are supported.
* If the path contains spaces, it must be wrapped in double-quote characters.
* The path `\TigerConnect` will be added to the end of the supplied argument.

`/run-at-startup=true`
* If the Admin installer is executed, this option controls whether to automatically run the TigerConnect app at system startup.
* If the Single-click installer is executed, this option controls whether to automatically run the TigerConnect app after the current user logs in.

`/S`
* Do not show any prompts or UI during the installation process.

`/?` or `/h` or `/help`
* Show this webpage.

## Support

If you have any questions please reach out to the TigerConnect team at any time by visiting [https://tigerconnect.com/support/](https://tigerconnect.com/support/).
