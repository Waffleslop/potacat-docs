# IC-7610: the I/Q Port and HDSDR

**POTACAT does not read the IC-7610's I/Q port.** POTACAT stays on **[USB 1]**, as before. The I/Q port feeds a separate SDR program, HDSDR, which you can run beside POTACAT on Windows. This page explains how to set that up, from Icom's own guides.

For CAT and audio setup of the IC-7610 itself, see [Icom IC-7300 & Family](rig-ic-7300.md#ic-7610).

## The two USB ports

| Port | What it carries | Who uses it |
|---|---|---|
| **[USB 1]** (type B) | CAT (CI-V) and the radio's sound card | POTACAT: CAT, audio, FT8, CW keying and its band scope |
| **[USB 2]** (USB 3.0 type B, the blue socket) | The receiver's raw I/Q signal, 1.66 MHz wide, from the MAIN or the SUB receiver | HDSDR, through Icom's driver package |

The two programs use different cables, so they don't compete for a COM port. In HDSDR you get a 1.66 MHz wide waterfall of the band, or an extra receiver.

## What you need

- IC-7610 firmware **1.20 or later**. Section 13 of the IC-7610 Advanced manual shows how to check and update it.
- A Windows PC with a **USB 3.0** port. Icom lists Windows 7, 8.1 and 10. Plug straight into the PC, never through a hub.
- A **USB 3.0 A-to-B cable**, as short as practical. Icom doesn't supply one, and notes that a long cable can be recognised by the PC and still not work.
- **HDSDR**, free from [hdsdr.de](https://www.hdsdr.de/). Icom tested version 2.76a.
- Icom's **USB I/Q Package for HDSDR** for the IC-7610, from Icom's support downloads. It holds the driver and `ExtIO_IC7610.dll`.

## Steps

Install in this order.

> **Warning:** Don't connect **[USB 2]** until step 3 is done.

1. **Check the firmware** is 1.20 or later. Update it first if not.
2. **Install HDSDR.** Note the folder it installs to, normally `C:\Program Files\HDSDR`.
3. **Install the USB I/Q Package.** Unzip it and run `setup64.exe` (64-bit Windows) or `setup32.exe`. Choose the language and check the destination is the HDSDR folder (use **Browse** if HDSDR went elsewhere). Click **Install**, and **Install** again at the Windows Security prompt.
4. **Turn the radio off.** Connect the USB 3.0 cable from **[USB 2]** to the PC, then turn the radio on. Windows finishes the driver.
5. **Check the driver.** In Device Manager, **Universal Serial Bus controllers** should list **IC-7610 I/Q OUT Port**. If it doesn't, run the package installer again.
6. **Start HDSDR.** If it asks which ExtIO to load, pick **ExtIO_IC7610.dll**.
7. In HDSDR, click **ExtIO** to open the IC-7610 I/Q Settings window:
   - **MAIN/SUB:** the receiver to watch. Choosing SUB turns Dualwatch on.
   - **Sync Mode:** **Only HDSDR sync** for a waterfall that follows the radio, or **Independent Tune in HDSDR** to use HDSDR as an extra receiver.
   - **Sampling Rate:** 1.92 MHz (BW 1.66 MHz) is the default. Pick a lower rate if the audio stutters.
8. Click **Soundcard** and pick your PC speaker. Click **Bandwidth** and set **Output Sampling Rate** to **12000**, which is enough for SSB.
9. Click **Start**. The waterfall shows the band around the radio's frequency. Click anywhere in it to listen there in HDSDR. The radio stays where it is.

If no sound comes out, choose **Options > Output Channel Mode for RX > AF to Both channels**.

## Using it with POTACAT

Leave POTACAT on **[USB 1]** exactly as before: **Settings > My Rigs**, Radio Model IC-7610, CI-V address `98h`.

| Sync Mode in HDSDR | When POTACAT moves the radio |
|---|---|
| **Only HDSDR sync** | HDSDR's centre follows the radio. Click a spot in POTACAT and the waterfall recentres on it. |
| **Independent Tune in HDSDR** | HDSDR keeps listening on its own frequency, as long as that frequency stays inside the 1.66 MHz window. |

- HDSDR's own **Lock** button and **Options > Misc Options > Tune fixed to 'LO <-> Tune Offset'** work against Sync Mode. Leave both off unless Sync Mode is **Only HDSDR sync**.
- **OVF** in the I/Q Settings window means the input is too strong. Turn the preamp off, add ATT, lower the RF gain, or turn DIGI-SEL on. All of these are in that window.

## CW Skimmer

Icom's "IC-7610 HDSDR Operating Guide" describes two ways to feed CW Skimmer from HDSDR. Follow Icom's guide for those; it is with the package on Icom's support downloads.

## What this is not

- **Not Mac or Linux.** Icom's driver package is Windows only.
- **Not POTACAT's band scope.** POTACAT's IC-7610 band scope and audio come over [USB 1].
- **No transmit through HDSDR.** The I/Q port is receive, plus a few receiver settings.

## Sources

This page is written from Icom's "Preparations for using the IC-7610 with the HDSDR application", "IC-7610 HDSDR Operating Guide" and "IC-7610 I/Q Output Reference Guide" (all 2018). Get the package and the guides from Icom.
