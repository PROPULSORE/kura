<!--
Release notes template for Kura. Copy it into the GitHub release.
Tag: vX.Y.Z. Asset names must stay exactly as below: the app's update check
and the README download links rely on them.
-->

## What's new

- 

## Fixes

- 

## Downloads

| Platform | File |
|---|---|
| Android | [kura-android.apk](https://github.com/PROPULSORE/kura/releases/download/vX.Y.Z/kura-android.apk) |
| Windows (installer) | [kura-setup-x64.exe](https://github.com/PROPULSORE/kura/releases/download/vX.Y.Z/kura-setup-x64.exe) |
| Windows (portable) | [kura-windows-x64.zip](https://github.com/PROPULSORE/kura/releases/download/vX.Y.Z/kura-windows-x64.zip) |
| Sync server, Linux 64-bit (optional) | [kura-server-linux-amd64](https://github.com/PROPULSORE/kura/releases/download/vX.Y.Z/kura-server-linux-amd64) |
| Sync server, Raspberry Pi (optional) | [kura-server-linux-arm64](https://github.com/PROPULSORE/kura/releases/download/vX.Y.Z/kura-server-linux-arm64) |
| Extension tool, Windows (for authors) | [kura-cli-windows-x64.zip](https://github.com/PROPULSORE/kura/releases/download/vX.Y.Z/kura-cli-windows-x64.zip) |

## How to update

- **Android:** download `kura-android.apk` and install it over the old version.
  Your data stays.
- **Windows (installer):** run `kura-setup-x64.exe`; it updates the installed
  version and keeps your data.
- **Windows (portable):** close Kura, then extract `kura-windows-x64.zip` over
  the old folder. Your data stays.

Windows may show a SmartScreen warning because Kura is not signed: click
**More info**, then **Run anyway**.

## SHA-256 checksums

```
<sha256>  kura-android.apk
<sha256>  kura-setup-x64.exe
<sha256>  kura-windows-x64.zip
<sha256>  kura-server-linux-amd64
<sha256>  kura-server-linux-arm64
<sha256>  kura-cli-windows-x64.zip
```

To check a file: on Windows `certutil -hashfile <file> SHA256`; on Linux or
macOS `sha256sum <file>`.
