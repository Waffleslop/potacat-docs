# Installation Issues

POTACAT is an open-source app distributed without a commercial code-signing certificate, so Windows, macOS, and some antivirus products treat it with suspicion the first time you run it. This page collects the platform-by-platform fixes for install, update, and first-start problems. If none of them helps, see [Report a Bug](../community--support.md#report-a-bug).

## Windows

### SmartScreen blocks the installer

Windows shows a "Windows protected your PC" warning because the installer is unsigned. Click **More info**, then **Run anyway**.

If **More info** doesn't appear: right-click the downloaded file → **Properties** → check **Unblock** → **OK**, then run it again.

### Double-clicking the installer does nothing

If the installer silently exits (or the install dialog appears briefly and vanishes), the file is usually being blocked. Work through these in order:

1. Right-click the `.exe` → **Properties** → check **Unblock** → **OK**
2. Right-click → **Run as administrator**
3. Open a Command Prompt in your **Downloads** folder and run the installer from there — any hidden error message will print to the console
4. Some users report that launching the file from File Explorer's **Downloads** folder works when clicking the browser's own download button does not

### Antivirus flags POTACAT (`IDP.generic` and similar)

POTACAT is an unsigned Electron app with a small user base, so reputation-based antivirus heuristics (Norton SONAR/IDP, ESET, and others) sometimes flag it. `IDP.generic` literally means "Identity Protection — generic heuristic" — it is not a specific threat detection. Some antivirus products also flag the bundled Cloudflare tunnel binary used by POTACAT Cloud; it's written in Go, and Go binaries commonly trip AV heuristics. These are false positives.

To get past it:

1. Restore the file from your antivirus quarantine and mark it as trusted
2. Add an exclusion for the POTACAT install folder — usually `C:\Users\<name>\AppData\Local\Programs\POTACAT`
3. If you want independent verification, upload the installer to [virustotal.com](https://virustotal.com) — and remember the code is fully open source on [GitHub](https://github.com/Waffleslop/POTACAT), so you can inspect exactly what it does

### The in-app updater hangs or loops

If **Restart to Update** crashes, hangs, or keeps re-offering the same version:

1. Open **Task Manager** and end the **POTACAT Launcher** process (the background update daemon)
2. Reopen POTACAT and run the update again
3. Press **F5** inside POTACAT to check for the latest update manually

> **Tip:** Every [GitHub release](https://github.com/Waffleslop/POTACAT/releases) includes a portable `.exe` in the release assets. It runs standalone, shares the same settings as the installed version, and is a handy way to try — or roll back to — a specific version without reinstalling.

## macOS

### "POTACAT is damaged and can't be opened"

This is Gatekeeper reacting to an unsigned app, not actual file corruption — the macOS equivalent of the Windows SmartScreen warning. After installing from the `.dmg`, clear the quarantine flag in Terminal:

```bash
xattr -d com.apple.quarantine /Applications/POTACAT.app
```

Then launch POTACAT normally.

### The app opens and immediately quits

If POTACAT launches and exits with no window, run the binary directly from Terminal so the real error prints to the console:

```bash
/Applications/POTACAT.app/Contents/MacOS/POTACAT
```

Startup crashes are often caused by something on your Mac conflicting with POTACAT (for example, another program already holding a network port). Copy the Terminal output into a bug report (see [Report a Bug](../community--support.md#report-a-bug)) — it usually identifies the culprit immediately.

### Microphone permission

The first time POTACAT needs audio input (digital modes, voice features), macOS asks for microphone access. If you denied it, decoding won't work — re-enable it under **System Settings → Privacy & Security → Microphone**.

## Linux

### Serial port permission denied

Your user needs to be in the `dialout` group to open serial ports:

```bash
sudo usermod -aG dialout $USER
```

The command prints nothing when it works; that is normal. Log out and back in (or restart) for the change to take effect. On some distributions the `tty` group is needed as well. To check, run `groups`: `dialout` should be in the list.

### Wrong file for the computer

A file for the wrong processor won't install or won't start. A PC or laptop needs the **amd64** (x86_64) file; a Raspberry Pi needs the **arm64** file, on a 64-bit operating system. `uname -m` tells you which you have. See [Installation: Which file?](installation.md#which-file).

### "How do I start it?"

A `.deb` or `.rpm` install adds POTACAT to your applications menu. An AppImage isn't installed: run it from the folder it is in. See [Installation: Start it](installation.md#start-it).

### AppImage won't start

- **Nothing happens when you double-click it.** It isn't executable yet. Run `chmod +x POTACAT-*.AppImage` once, then start it from a terminal with `./POTACAT-*.AppImage` so you can see any error.
- **An error about FUSE or `libfuse.so.2`.** The AppImage needs `libfuse2`: `sudo apt install libfuse2` on Debian, Mint and older Ubuntu. On Ubuntu 24.04 and later the package is called `libfuse2t64`.

Older builds could stop with a sandbox error like this:

```
The SUID sandbox helper binary was found, but is not configured correctly...
chrome-sandbox is owned by root and has mode 4755
```

Current builds handle this by themselves when they start. If you still see it, launch with the sandbox turned off and [report it](../community--support.md#report-a-bug):

```bash
./POTACAT-*.AppImage --no-sandbox
```

### Crashes at start on Wayland (Raspberry Pi OS Trixie and others)

Some Wayland desktops, including Raspberry Pi OS Trixie, crash POTACAT at start with a segmentation fault. Users report that starting the AppImage with the X11 back end gets past it:

```bash
./POTACAT-*.AppImage --ozone-platform=x11
```

### No transmit audio, or the radio's sound card isn't listed

- On Linux the radio's sound card often appears under its chip name, such as **PCM2901** or **PCM2903B**, rather than **USB Audio CODEC**. Pick that entry for the rig's audio input and output.
- If you see only the computer's built-in devices, check that the radio is plugged in and switched on, then restart POTACAT. The sound system (PipeWire or PulseAudio) has to see the device before POTACAT can.
- If the radio keys but puts out little or no power on FT8, SSTV or voice from ECHOCAT, raise the device's **output** level in your desktop's sound settings, then fine-tune with POTACAT's own level.

### Notes by distribution

These come from what users have reported, not from a test lab.

- **Linux Mint** — the most reports of POTACAT working. Use the `amd64.deb`.
- **Fedora** — use the `.rpm` or the AppImage. Users got it working, often after setting the radio's sound card output level in Fedora's sound settings.
- **Arch and Arch-based** — the AppImage works. A community package exists in the AUR; it can lag behind the newest release.
- **Ubuntu** — installs and runs; audio device setup is the step most likely to need attention (see above).
- **Raspberry Pi OS** — 64-bit only, with the `arm64` files. See [Small computers](#small-computers-and-chromebooks) and [Running Headless](headless.md).

### Small computers and Chromebooks

- **Raspberry Pi 4 and 5** — work with 64-bit Raspberry Pi OS and the `arm64` files. Users also report older boards (Pi 3B and 3B+) running it, more slowly. If you're new to POTACAT, get it running on a Windows/Mac/Linux desktop first, then move to the Pi; it makes troubleshooting much easier.
- **Pi Zero 2 and similar low-power boards** — marginal; expect sluggish performance.
- **Chromebooks** — effectively unsupported. The AppImage doesn't run usefully, and ChromeOS's Linux container can't pass through USB serial devices, so CAT control won't work.

To run a Pi with no monitor attached, see [Running Headless](headless.md).

## Where settings live (and factory reset)

POTACAT stores its settings outside the install folder, so they **survive uninstall and reinstall**:

| Platform | Settings folder |
|----------|-----------------|
| Windows | `%APPDATA%\POTACAT` (i.e. `C:\Users\<you>\AppData\Roaming\POTACAT`) |
| macOS | `~/Library/Application Support/POTACAT` |
| Linux / Raspberry Pi | `~/.config/POTACAT` (`/root/.config/POTACAT` when run as root) |

If POTACAT misbehaves even after a reinstall, a corrupt settings file is the likely cause. Deleting this folder resets POTACAT to a true first-run state.

> **Warning:** Deleting the settings folder erases all settings, rig configurations, and cached data — you'll set everything up again from scratch. Note where your ADIF log file lives (Settings → Logging) before deleting anything.

Advanced users can hand-edit `settings.json` inside this folder (for example, the rigs array). Never paste your raw `settings.json` into a bug report or Discord — it contains credentials. Use the **Report a Bug** button in Settings instead, which generates a safe, formatted report; see [Report a Bug](../community--support.md#report-a-bug).

## Getting a log without the window (headless / Raspberry Pi)

When POTACAT runs headless (no window, for example on a Raspberry Pi), there's no **Report a Bug** button. Send us its log file instead:

1. Restart POTACAT so the log starts clean.
2. Reproduce the problem: key up and talk, tap a spot, whatever isn't working.
3. On the Pi, copy the log somewhere easy to reach:

   ```
   cp ~/.config/POTACAT/session.log ~/potacat-log.txt
   ```

   If POTACAT runs as a system service under root, the log is at `/root/.config/POTACAT/session.log` instead; use `sudo cp /root/.config/POTACAT/session.log ~/potacat-log.txt`. If you can't find it, this searches for it:

   ```
   cp "$(find / -path '*POTACAT/session.log' 2>/dev/null | head -1)" ~/potacat-log.txt
   ```

4. Copy it to your computer. In PowerShell, Command Prompt or Terminal there:

   ```
   scp <user>@<pi-address>:~/potacat-log.txt .
   ```

5. Attach `potacat-log.txt` in Discord's **#bug-report** channel or on a GitHub issue, as described in [Report a Bug](../community--support.md#report-a-bug).

> **Note:** Unlike **Report a Bug**, the raw log isn't tidied up: it shows your callsign and folder paths. Settings and passwords are never written to it, but read it over first if that matters to you.

The previous run's log is kept as `session.log.old` in the same folder, in case the problem happened before your last restart. The same files exist on every system, in the settings folder (see [above](#where-settings-live-and-factory-reset)): `%APPDATA%\POTACAT\` on Windows and `~/Library/Application Support/POTACAT/` on macOS.

## Running from source

Most users should use the installers from [potacat.com](https://potacat.com) or [GitHub Releases](https://github.com/Waffleslop/POTACAT/releases). Running from source is for power users who want fixes as soon as they're committed, between installer releases.

You'll need **Node.js 20+** and **Git** (plus Visual Studio Build Tools on Windows; `sudo apt install build-essential python3 libudev-dev` on Debian/Ubuntu):

```bash
git clone https://github.com/Waffleslop/POTACAT.git
cd POTACAT
npm install
npm start
```

To update later, run `git pull` in the `POTACAT` folder, then `npm start` again. Optionally, `npm run build-ft8` compiles the native FT8 decoder (10–50x faster decoding than the fallback).

Common gotchas:

- **`'git' is not recognized`** (Windows) — install [Git for Windows](https://git-scm.com/download/win) and select **"Git from the command line and also from 3rd-party software"** during setup. A reboot may be needed for the `PATH` change to take effect.
- **"You have node version 18 and need version 20"** — your distro's packaged Node is too old. Install Node 20+ via [nvm](https://github.com/nvm-sh/nvm) or NodeSource.
- Deprecation warnings during `npm install` are noise — they are not the reason a build failed.
