# Revival Cast - Releases

Download hosting for **Revival Cast**, church presentation software by
[Visionary Technologies Enterprise](https://www.vteofficial.com).

This repository contains **release packages only**. The application's source is
maintained in a private repository and is not published here.

---

## Download

Get Revival Cast from the official website:

**https://revivalcast.vteofficial.com**

The website always offers the current version and keeps previous versions
available, with their notes. Downloading from there is preferable to picking a
file from this repository directly, because it is the address the application's
own updater uses.

The published version is whatever the Releases page above lists as Latest. This
file deliberately does not repeat it, so it cannot fall out of date.

## What a release contains

| File | Purpose |
| --- | --- |
| `RevivalCastSetup_v<version>.exe` | The Windows installer. This is the file the in-app updater downloads and runs. |
| `release.json` | The update manifest. It records the version, the download address and the installer's SHA-256, so the application can verify what it downloads before running it. |

The installer is the only package published. There is no portable build.

## Requirements

- Windows 10 64-bit (version 1809 or newer), or Windows 11
- 64-bit (x64) processor
- 4 GB RAM, 8 GB recommended for large presentations
- 500 MB free disk space
- Administrator rights to run the installer
- A second display or projector for live output (optional: the operator view
  runs on one screen)

Nothing else needs installing. The installer contains the .NET runtime the
application uses, and there is no account to create.

## Installing and upgrading

Run `RevivalCastSetup_v<version>.exe` and follow the prompts. It installs to
`C:\Program Files\RevivalCast` and adds a Start Menu entry.

To upgrade, run a newer installer over the top. Inno Setup matches the installed
copy by application identity and upgrades in place, so there is no need to
remove the current version first, and your services and libraries are left
untouched. The installer closes a running copy and restarts it afterwards.

**Windows may show a SmartScreen prompt** for a new release, because the
installers are not yet code-signed. Choose **More info**, then **Run anyway**.

## Verifying a download

Every release's `release.json` records the SHA-256 of its installer. To check a
file you have downloaded:

```powershell
Get-FileHash .\RevivalCastSetup_v<version>.exe -Algorithm SHA256
```

Compare the result with the `sha256` value in that release's `release.json`. If
they differ, do not run the file.

## Automatic updates

The application checks for updates from
`https://revivalcast.vteofficial.com/updates/latest.json`, which is served by
the project's website. When a newer version is published:

1. The application offers the update and shows its release notes.
2. Nothing is downloaded or installed without approval.
3. The installer is checked against the published SHA-256 before it runs. A file
   that does not match is discarded and the installed version is left alone.
4. The open service is saved before the installer starts, and installation is
   refused if that save fails.

The manifest records the download address on the project's own domain, which
redirects to the file in this repository. That indirection means the address
compiled into shipped software never has to change if hosting moves.

You can check manually with **Help > Check for Updates**.

## Support

- User manual: **https://revivalcast.vteofficial.com/docs/RevivalCast-User-Manual.pdf**
- Email: visionarytechnologiesent@gmail.com
- Website: **https://www.vteofficial.com**

Please include the version shown in **Help > About Revival Cast**. If the
application closed unexpectedly, the log is at:

```
%AppData%\RevivalCast\crash.log
```

## Licence

Revival Cast is proprietary software owned by Visionary Technologies
Enterprise. Use is governed by the end user licence agreement included with the
application, which is presented during installation and installed to:

```
C:\Program Files\RevivalCast\LICENSE.txt
```

Downloading the software does not grant any licence beyond that agreement.
