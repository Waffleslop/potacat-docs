# Yaesu SCU-LAN10 (Experimental)

> **Experimental, new in POTACAT 1.14.0.** It was built from the published protocol description. From 1.14.6, transmit audio over the network has been tested on an FT-710. If you try it, please send a report from **🐞 Report a Bug** in the Settings sidebar: see [Report a Bug](../community--support.md#report-a-bug).

POTACAT can connect to a Yaesu **FTDX10**, **FT-710** or **FTDX101D/MP** over the network through Yaesu's **SCU-LAN10** unit, with no USB cable to the computer.

## What works, and what doesn't

- **Works:** CAT control (frequency, mode, spot clicks, the VFO window and meters) and **receive audio** over the network, for FT8 decoding, SSTV, the waterfalls, the VFO window's speaker and listening from ECHOCAT.
- **Band scope:** the radio's scope comes over the LAN too, in the Band Scope window, the FT8 window's scope strip and ECHOCAT, with the span read from the radio. On the FTDX10 and FTDX101, the span codes are taken from the FT-710's, so the span shown may be off.
- **Transmit audio over the network, from 1.14.6.** With **Audio source** set to Yaesu LAN audio, voice, voice macros, JTCAT FT8 and FT4, Tune, SSTV and CW text go over the network, and JTCAT keeps hearing after the first transmission. Before 1.14.6 POTACAT would not key the radio while its audio came over the network.
- **Doesn't work: Winlink over LAN audio.** For Winlink, set **Audio source** to the radio's own USB sound card on this computer.
- **Mute the radio's speaker, from 1.14.6.** Tick **Mute the radio's speaker monitor and CW sidetone while POTACAT has the radio** in the rig's settings (FT-710 and FTDX10). POTACAT sets the radio's monitor off and its level to 0 in each mode you use, and puts every mode back when it disconnects or quits.

## Before you start

**Radio firmware,** at least:

| Radio | MAIN | DISPLAY | SDR |
|---|---|---|---|
| FTDX10 | V01-01 | V01-01 | V01-00 |
| FT-710 | V01-11 | V01-08 | V01-04 |
| FTDX101D/MP | V01-14 | V01-06 | V02-03 |

**Radio menus,** as Yaesu's SCU-LAN10 setup asks:

| Menu | Set to |
|---|---|
| CAT RATE | `38400` (`115200` over the LAN) |
| CAT TIMEOUT TIMER | `10 ms` |
| CAT RTS | `ON` |

**Close PCC-LAN10 or FT-Control.** The SCU-LAN10 takes one program at a time.

> **Warning:** Use the SCU-LAN10 on your home network, or through [Tailscale](echocat-connectivity.md#path-3-tailscale-full-walkthrough) or a VPN when you're away. **Never open its ports to the internet**: its link isn't really encrypted.

## Set it up

1. Open **Settings > My Rigs** and edit your radio (or add one).
2. Pick the radio in **Radio Model**, then choose **Yaesu LAN (SCU-LAN10), experimental**.
3. **Address:** the unit's IP address. From the factory it's `192.168.49.1`.
4. **Base port:** `50000`, unless you changed it on the unit. It's the first of four UDP ports; CAT, audio and scope follow it.
5. **User** and **Password:** the ones you set on the unit. Leave both blank for the factory login.
6. Click **Test Connection**. It should log in, name your radio and show its frequency.
7. For audio over the network, set **Audio source** to the Yaesu LAN audio option, then **Save**.

## If it doesn't connect

- A wrong password gets no reply at all from the unit, so a login that times out usually means the address, port or password is wrong.
- Check that PCC-LAN10, FT-Control or another copy of POTACAT isn't still connected to the unit.
- Check the radio's firmware and CAT menus above.

## Help check the band scope

The first time scope data arrives, POTACAT saves one raw scope frame to a file named `sculan10-scope-frame.bin` in its settings folder; the log names the full path. Attach that file to your bug report, so the scope can be checked against a real radio.
