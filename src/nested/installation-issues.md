# Installation Issues

POTACAT is an open-source app distributed without a commercial code-signing certificate, so Windows, macOS, and some antivirus products treat it with suspicion the first time you run it. This page collects the platform-by-platform fixes for install, update, and first-start problems.

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

Startup crashes are often caused by something on your Mac conflicting with POTACAT (for example, another program already holding a network port). Copy the Terminal output into a bug report — it usually identifies the culprit immediately.

### Microphone permission

The first time POTACAT needs audio input (digital modes, voice features), macOS asks for microphone access. If you denied it, decoding won't work — re-enable it under **System Settings → Privacy & Security → Microphone**.

## Linux

### Serial port permission denied

Your user needs to be in the `dialout` group to open serial ports:

```bash
sudo usermod -aG dialout $USER
```

Log out and back in for the change to take effect. On some distributions the `tty` group is needed as well.

### AppImage won't start

The AppImage needs `libfuse2` (`sudo apt install libfuse2` on Debian/Ubuntu-based distros).

Some users on certain distributions hit a sandbox error like:

```
The SUID sandbox helper binary was found, but is not configured correctly...
chrome-sandbox is owned by root and has mode 4755
```

The usual workaround for this Electron/Chromium sandbox issue is to launch the AppImage with the sandbox disabled:

```bash
./POTACAT-*.AppImage --no-sandbox
```

### Small computers and Chromebooks

- **Raspberry Pi 5** — works. If you're new to POTACAT, get it running on a Windows/Mac/Linux desktop first, then move to the Pi; it makes troubleshooting much easier.
- **Pi Zero 2 and similar low-power boards** — marginal; expect sluggish performance.
- **Chromebooks** — effectively unsupported. The AppImage doesn't run usefully, and ChromeOS's Linux container can't pass through USB serial devices, so CAT control won't work.

## Where settings live (and factory reset)

POTACAT stores its settings outside the install folder, so they **survive uninstall and reinstall**:

| Platform | Settings folder |
|----------|-----------------|
| Windows | `%APPDATA%\POTACAT` (i.e. `C:\Users\<you>\AppData\Roaming\POTACAT`) |
| Linux | `~/.config/potacat` |

If POTACAT misbehaves even after a reinstall, a corrupt settings file is the likely cause. Deleting this folder resets POTACAT to a true first-run state.

> **Warning:** Deleting the settings folder erases all settings, rig configurations, and cached data — you'll set everything up again from scratch. Note where your ADIF log file lives (Settings → Logging) before deleting anything.

Advanced users can hand-edit `settings.json` inside this folder (for example, the rigs array). Never paste your raw `settings.json` into a bug report or Discord — it contains credentials. Use the **Report a Bug** button in Settings instead, which generates a safe, formatted report.

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
