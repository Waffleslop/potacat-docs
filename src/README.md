# POTACAT

**POTACAT** is a free, open-source desktop application for amateur radio operators who want to hunt Parks on the Air (POTA) activators, chase SOTA summits, work DX, and operate their radio remotely from a phone.

Built by **Casey Stanton, K3SBP** and a growing community of contributors.

## See It in Action

Three videos from other operators' channels show POTACAT and ECHOCAT in use:

- **[The Free App Remote Hams Are Switching To - POTACAT](https://www.youtube.com/watch?v=QyjFec5rQF0)**, on KM4ACK's channel. Start here.
- **[How To Do HF Ham Radio While Grocery Shopping](https://www.youtube.com/watch?v=3DuQkHkYB8w)**, on Ham Radio Tube.
- **[POTACAT - FREE Remote and Rig Control Software for your Radio](https://www.youtube.com/watch?v=U4p4HK-u5wo)**, on Ham Radio 2.0.

## How It Started

POTACAT began with a simple idea: see all the live POTA spots on one page and one-click tune my FlexRadio to any spot. No more copying frequencies by hand, no more fumbling between browser tabs and radio software. Click a row, radio tunes, start calling.

That first version was a weekend project. Then people wanted SOTA spots too. Then DX Cluster integration, DX expedition tracking, and Reverse Beacon Network. Then logbook forwarding, ADIF export, and QSO logging. Then WWFF and LLOTA spots. Then respotting, panadapter integration, and a full CW keyer. Every feature was driven by real operators asking "can POTACAT do this?" and the answer kept being yes.

## What It Does Today

- **Live spot aggregation** from POTA, SOTA, WWFF, LLOTA, DX Cluster, RBN, and PSKReporter. See [Spot Sources](spot-sources.md).
- **One-click QSY** to any spot with CAT control for FlexRadio, Icom, Yaesu, Kenwood, Elecraft, Xiegu, QRP Labs, and Hamlib-supported rigs, and Zeus or Thetis SDRs over TCI. See [Radio Setup](radio-setup.md).
- **Map and table views** with band/mode filters, distance, bearing, and beam heading
- **QSO logging** with ADIF export and forwarding to Log4OM, HamRS, Ham Radio Deluxe, N3FJP, DXKeeper, Wavelog, MacLoggerDX, QRZ Logbook, World Radio League, and SOTAdata
- **JTCAT** -- a built-in FT8/FT4 engine (no WSJT-X required) with waterfall, decode panel, and auto-QSO. See [JTCAT](nested/jtcat.md).
- **Winlink email** over the internet, ARDOP, packet and VARA, with the Winlink Standard Forms from 1.14.7. See [Winlink Email](nested/winlink.md).
- **APRS**, new in 1.14.7: a map of stations near you, listening on your own radio, beacons, messages and an iGate. See [APRS](nested/aprs.md).
- **SSTV**, and **FreeDV digital voice** receive. See [SSTV](nested/sstv.md) and [FreeDV / PSKReporter](nested/freedv--pskreporter.md#freedv-digital-voice-receive).
- **CW Keyer** with MIDI paddle support, remote CW from your phone, and text macros
- **SmartSDR and TCI panadapter spots** so you can see activators on your waterfall
- **DXCC Tracker**, DX expedition board, solar propagation, band activity heatmap
- **Scan mode** to auto-tune through filtered spots like scanning a police scanner
- **Tune links**: a `potacat://` link on a web page tunes your radio. See [Tune Links](nested/tune-links.md).

For what changed in each version, see [Release Highlights](changelog.md).

## ECHOCAT: Remote Radio for Everyone

**ECHOCAT** is POTACAT's remote radio feature. Use the ECHOCAT app for iOS and Android, or open ECHOCAT Web in your phone's browser, and you have control of your radio: tune, transmit SSB, send CW, and run FT8 -- all from your phone. See [ECHOCAT](echocat.md).

**We are democratizing remote radio.**

Not everyone can afford a FlexRadio with SmartLink or the latest internet-connected transceiver. Remote operation shouldn't be a luxury. Our mission is to bring remote SSB, FT8, and CW to as many radios and operators as possible. ECHOCAT runs on hardware as modest as a Raspberry Pi connected to a Xiegu G90. If your radio has a serial port or USB, you can probably run it remotely with POTACAT.

There are three ways for the phone to reach your shack: your home network, a VPN like Tailscale, or the POTACAT Cloud tunnel. The first two need no account. POTACAT Cloud is optional; it adds a personal address with no VPN and no port forwarding, and [Share Your Rig](echocat.md#share-your-rig), which lends your radio to another operator with a timed Guest Pass. You can also [run your shack from another POTACAT](nested/remote-desktop.md).

## Get Involved

POTACAT is in active development. New features ship weekly. We build what the community asks for.

- **Discord** -- Join us at [potacat.com/discord](https://potacat.com/discord) to report bugs (see [Report a Bug](community--support.md#report-a-bug)), request features, get help, and chat with fellow operators
- **GitHub** -- Source code, issues, and pull requests at [github.com/Waffleslop/POTACAT](https://github.com/Waffleslop/POTACAT)
- **Support the project** -- Keep POTACAT alive and growing by becoming a supporting member at [buymeacoffee.com/potacat](https://buymeacoffee.com/potacat)

73 de K3SBP
