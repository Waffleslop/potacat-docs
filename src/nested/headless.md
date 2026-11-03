# Running Headless (Raspberry Pi or a PC with No Monitor)

> **Warning:** **Draft, untested.** This page was written from POTACAT's code and from what users have reported. Nobody has yet run these exact steps on a Raspberry Pi 4 or 5 with no monitor attached. If something here doesn't work for you, tell us on Discord and we'll fix the page.

Many operators keep POTACAT on a small computer by the radio (a Raspberry Pi, a mini PC, a spare laptop) and operate from somewhere else with [ECHOCAT](../echocat.md) or [another POTACAT](remote-desktop.md). This page explains what "headless" means for POTACAT, what still needs a screen, and how to start it.

## What headless means here

**POTACAT has no true headless mode.** It is a desktop app. Starting it with `--headless` runs the **full app with its window hidden**: the same program, the same memory use and the same settings as when you can see it. It does not turn POTACAT into a server that runs without a desktop.

What the `--headless` flag changes:

- The main window stays hidden.
- ECHOCAT is switched on, whatever the setting says.
- A moment after start, the ECHOCAT addresses are printed in the terminal under `Connect via ECHOCAT:`, one per network, in the form `https://<address>:7300` (7300 is the default port; a different port set in **Settings > ECHOCAT** is used instead).
- POTACAT keeps running when no window is open.
- The crash dialog is not shown.

Everything else (CAT control, spots, FT8, the CW keyer, logging, ECHOCAT) works as it does with the window showing.

## Do you need it?

Probably not. There are three ways to run a station from somewhere else, and most users run the first two:

| Setup | What it is | When it fits |
|---|---|---|
| **A shack PC plus ECHOCAT** | POTACAT runs normally on a computer at the radio, with its window open on that computer's desktop. You operate from a phone, a browser, or [another POTACAT](remote-desktop.md). | Almost always. The shack PC can sit in a corner with its screen off. |
| **A computer with no monitor, reached by remote desktop** | The same, but you see the desktop with VNC, Raspberry Pi Connect or another remote desktop when you need to change something. | A Pi or mini PC with nothing plugged into its display port. |
| **The `--headless` flag** | The second setup, with POTACAT's window hidden and the ECHOCAT addresses printed at start. | You want no POTACAT window on that desktop at all. |

All three still need a desktop session running on that computer.

## Hardware

- **Raspberry Pi 4 or 5**, with **64-bit** Raspberry Pi OS. POTACAT's Pi builds are `arm64` only, so a 32-bit OS won't run them.
- Users also report running POTACAT on a **Pi 3B or 3B+**, more slowly; a mini PC; a small form factor PC; and a Linux virtual machine. A Pi Zero 2 is marginal.
- If you're new to POTACAT, set it up on a Windows, Mac or Linux desktop first, then move to the Pi. Troubleshooting is much easier with a screen.

## Install

Install the `arm64` build and give yourself access to the radio's serial port, as in [Installation: Linux](installation.md#linux):

```bash
cd ~/Downloads
sudo apt install ./potacat_*_arm64.deb
sudo usermod -aG dialout $USER
```

Log out and back in after the last line.

## First setup needs a screen

Plug in a monitor, or connect with remote desktop (VNC or Raspberry Pi Connect), for the first run. In POTACAT, with its window showing:

1. Enter your callsign and set up your radio (**Settings > My Rigs**), including its audio devices.
2. Turn on ECHOCAT.
3. Pair your phone, or another POTACAT.

#### "There's no QR code to scan?"

Right: with the window hidden there is nowhere to show the pairing QR code, and the **Approve** prompt for tap-to-pair appears on the Pi's screen. **Pair while you can see the desktop**, with a monitor or remote desktop. Once a phone is paired it reconnects by itself, with POTACAT's window hidden or not.

ECHOCAT Web in a browser needs no pairing: open the address POTACAT prints (or shows in **Settings > ECHOCAT**) and, if you set one, enter the password.

## Keep a desktop session running

POTACAT needs the Pi's desktop to be running, even when no monitor is attached and the window is hidden. Its hidden window and the audio link to the radio both run inside that desktop session.

- Set the Pi to **boot to the desktop** and **log in automatically** (in Raspberry Pi OS: **Raspberry Pi Configuration > System**).
- Use a Raspberry Pi OS image that includes the desktop. Starting POTACAT from a plain ssh session, with no desktop running, is not supported.

## Start it

From a terminal **on the Pi's desktop** (or a remote desktop session):

```bash
potacat --headless
```

POTACAT starts with no window and prints the ECHOCAT addresses a moment later. Open one of them in a browser, or connect with the ECHOCAT app.

On an AppImage, run it from its folder instead: `./POTACAT-*-arm64.AppImage --headless`.

> **Note:** Use POTACAT 1.13.9 or later with a `.deb` install. Before 1.13.9, `potacat` typed in a terminal stopped with an error that it couldn't find `potacat.bin` (starting from the applications menu was not affected). On an older version, start it by its full path: `/opt/POTACAT/potacat --headless`.

On Raspberry Pi OS Trixie, if POTACAT crashes at start, users report that adding `--ozone-platform=x11` gets past it (see [Installation Issues](installation-issues.md#crashes-at-start-on-wayland-raspberry-pi-os-trixie-and-others)).

## Start at boot

In POTACAT, open **Settings > Station** and tick **Launch POTACAT when this computer starts**. POTACAT then opens each time the desktop starts, with its window showing; that is the simplest setup and the one users run. Combined with booting to the desktop and logging in automatically, the Pi comes back on its own after a power cut.

This starts POTACAT normally, not with `--headless`. It needs the desktop login described above.

## Changing settings later

Most settings are only in the desktop window. To change them, connect with remote desktop (VNC or Raspberry Pi Connect), or plug in a monitor. If POTACAT was started with `--headless`, quit it and start it normally to see the window.

ECHOCAT covers what you need to operate (tuning, mode, power, audio, FT8, CW, logging, some rig settings), but not all of POTACAT's settings.

## Audio

- Choose the radio's sound card for the rig's audio input and output in **Settings > My Rigs**. On Linux it often shows under its chip name, such as **PCM2901** or **PCM2903B**, rather than **USB Audio CODEC**.
- If the radio keys but puts out little or no power, raise the device's output level in the Pi's sound settings.
- **Digirig DR-891 with an FT-891 keying up again and again on its own:** one user stopped it by muting the interface's right audio channel in the Pi's sound settings, so the radio's VOX no longer heard it.

## Getting a log or reporting a bug

With the window hidden there is no **Report a Bug** button. See [Getting a log without the window](installation-issues.md#getting-a-log-without-the-window-headless--raspberry-pi) to copy POTACAT's log off the Pi, then post it as described in [Report a Bug](../community--support.md#report-a-bug).

## Still open

These are known gaps. If you get one of them working, please share how on Discord.

- `--headless` on a `.deb` install, on the AppImage, and on a Pi 4 and Pi 5 with no monitor: not yet tested end to end.
- Transmit audio from a Pi 4 over Tailscale: one open report of no TX audio.
