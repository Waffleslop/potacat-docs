# Installation

1. Download the latest installer from [potacat.com](https://potacat.com) or the [GitHub Releases](https://github.com/Waffleslop/POTACAT/releases) page
2. Run the installer (`.exe` for Windows, `.dmg` for macOS; for Linux see [below](#linux))

   **System requirements:** Windows 10 or later; **macOS 12 (Monterey) or later**; 64-bit Linux on a PC or a Raspberry Pi 4 or 5.
3. **Windows SmartScreen:** Since POTACAT is not code-signed by Microsoft, Windows may show a SmartScreen warning. Click **"More info"** then **"Run anyway"** to proceed
4. A portable version (no install) is also available on the Releases page — it uses the same settings location as the installer version

> **Tip:** If "More info" doesn't appear, right-click the downloaded file → Properties → check "Unblock" → OK, then try again.

## Linux

### Which file?

Every release has a file for each kind of Linux computer. An ordinary PC or laptop (Intel or AMD) is **amd64**, also called x86_64. A Raspberry Pi or other ARM board is **arm64**, also called aarch64. Not sure? Run `uname -m` in a terminal: `x86_64` means amd64, `aarch64` means arm64.

| Your computer | File |
|---|---|
| Linux Mint, Ubuntu or Debian on a PC | `potacat_<version>_amd64.deb` |
| Fedora on a PC | `potacat-<version>.x86_64.rpm` |
| Any other Linux on a PC | `POTACAT-<version>.AppImage` (the one without `arm64`) |
| Raspberry Pi 4 or 5, other ARM boards | `potacat_<version>_arm64.deb` or `POTACAT-<version>-arm64.AppImage` |

The ARM builds need a **64-bit** operating system. There is no 32-bit build.

### Install it

Open a terminal and go to the folder the file downloaded to (usually `Downloads`):

```bash
cd ~/Downloads
```

Then, for a `.deb` (Mint, Ubuntu, Debian, Raspberry Pi OS):

```bash
sudo apt install ./potacat_*_amd64.deb
```

On a Raspberry Pi, use `./potacat_*_arm64.deb` instead. The `./` matters: it tells `apt` to install the file in this folder rather than look for a package online. If `ls *.deb` shows more than one version, type the full file name.

For an `.rpm` (Fedora):

```bash
sudo dnf install ./potacat-*.x86_64.rpm
```

For an AppImage, nothing is installed. Make it executable once, then run it:

```bash
chmod +x POTACAT-*.AppImage
./POTACAT-*.AppImage
```

### Start it

A `.deb` or `.rpm` puts **POTACAT in your applications menu**. Start it from there, like any other program.

An AppImage is a single file you keep wherever you like. Double-click it, or run it from its folder as above. If double-clicking does nothing, run it from a terminal: the error it prints says why (usually FUSE, see [Installation Issues](installation-issues.md#appimage-wont-start)).

### Let POTACAT reach the radio

To open the radio's USB serial port for CAT control, your user must be in the `dialout` group. Run this once:

```bash
sudo usermod -aG dialout $USER
```

It prints nothing when it works. Log out and back in (or restart) for it to take effect.

### Pick the radio's sound card

On Windows the radio's audio usually appears as **USB Audio CODEC**. On Linux the same device often shows under its chip name instead, such as **PCM2901** or **PCM2903B**. That is the one to pick for the rig's audio input and output. If the radio keys up but transmits little or no power, raise the device's output level in your desktop's sound settings as well as in POTACAT.

### Updating

To install a newer version, download its file and install it the same way. Your settings live in `~/.config/POTACAT`, outside the install, so they are kept.

**Having trouble?** See [Installation Issues](installation-issues.md) for platform-by-platform fixes — antivirus false positives, the macOS "app is damaged" message, Linux serial port permissions and AppImage problems, updater hangs, and factory reset. Running POTACAT on a Raspberry Pi with no monitor? See [Running Headless](headless.md).
