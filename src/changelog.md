# Release Highlights

This page summarizes major POTACAT and ECHOCAT releases — it is not an exhaustive list of every patch.

### v1.9.4 — July 2026

- **13 Colonies** fixes across desktop and mobile, plus a 13 Colonies tracking list with notifications in the mobile `CNTSTS` tab.
- Connectivity bug fixes; the Tailscale certificate is no longer cached at startup (fixes Tailnet account changes).
- Matching mobile OTA updates — update both desktop and app.
- JTCAT fix for `RR73` decoded as a grid square; continued FT8 parity work with WSJT-X.
- iOS QR-scan fix for macro-lens iPhones; SSTV and Activator-mode updates on mobile.

### v1.9.2 + ECHOCAT mobile v1.1 — June 2026

- **Straight Key** on-screen CW button in the mobile app.
- Fully **customizable VFO screen** — hide and reorder elements.
- Improved pairing: one click to connect when paired with POTACAT v1.9.2.
- Up to **25 voice/CW macros**, synced across devices (older on-phone macros are wiped).
- Android landscape mode.

### ECHOCAT for Android — June 26, 2026

- ECHOCAT app live on **Google Play** (`co.cmox.echocat`) — $9.99 one-time purchase, includes all updates.
- Known bug at launch: connecting via "Discovered" was broken — use the QR scan instead.

### v1.8.16 — June 2026

- **Instant pairing** for Cloud subscribers: log in on any device and connect to your shack, over Tailscale or POTACAT Cloud off-LAN.
- **WSPR TX/RX** working; the **idle agent** can decode SSTV or WSPR (Settings > Station), with WSPR reports sent to PSKReporter.
- IC-7100 rig layer.

### v1.8.14 — June 2026

- **Late-start FT8 TX** — join a slot roughly 7 seconds late with a shortened reply (WSJT-X parity).
- **A-priori (AP) decoding** in JTCAT; day/night line added to the JTCAT map.
- **FT-710 ATU** control over CAT; per-rig audio settings under Settings > Radio.
- Remote **Stop Scan** from ECHOCAT; Linux arm64 build.

### v1.8.6 — June 10, 2026 — POTACAT Cloud launch

- **POTACAT Cloud** subscription: $5/mo or $50/yr with a free trial — cloud log backup, multi-device logging, parks-worked sync, and the **Cloud Tunnel** (`<callsign>.potacat.com`, no Tailscale required).
- **Cloud Sharing** stack: desktop-to-desktop pairing, **Share My Rig** links (start-now or scheduled, optional anonymous guests, 30-day guest link cap), and **tap-to-pair** on the LAN.
- Follow-ups in v1.8.7–v1.8.9: revoking access now kicks live sessions instantly, hardened cloud backup download, and a **TURN relay** for CGNAT (including double-CGNAT/Starlink).
- **Charcoal** dark theme (Settings > Display), Contests "What's Next" redesign, color-coded logbook columns with `Ctrl` `+`/`−` zoom.
- `STATION_CALLSIGN` now written on every QSO (LoTW / Part 97.119 attribution); **Flex per-band antenna mapping**.

### ECHOCAT for iOS — June 8, 2026

- ECHOCAT app live on the **App Store** — $9.99 one-time purchase, includes all updates.
- **ECHOCAT Web** continues to work and remains free; Tailscale remains an option.

### v1.6 — May 2026

- "Whole Lotta Things Working Well": initial **keyer support in the iOS/Android apps** — TinyMIDI, VBand, Vail, and HaliKey MIDI.
- **Flex Radio direct connection without SmartSDR** plus full **WinKeyer** support (May 21) — enables AetherSDR use with POTACAT.
- **POTACAT Cloud Tunnel** first working (June 2): connect a phone to the rig with no Tailscale — the foundation for rig swapping.

### v1.5.16 — May 2026

- Initial foundation for the **iOS and Android apps**; tester builds followed in the Hamvention build.
- **WebSDR + KiwiSDR** RX "finally working as intended" — listen on a remote SDR while transmitting on your own rig.
- FT8 timing and respot-logging fixes; ragchew logger pop-out with `Ctrl+F1`/`Alt+F1` hotkeys.

### v1.5.2 — April 2026

- "Mega GitHub Issue Squashing" release; POTA.app sync phase 1, with Cloud users auto-syncing POTA parks-worked.
- **Auto-SSTV RX on idle** (default on, 90-minute timeout); SSTV **Scottie S2** support.
- **CI-V over TCP**; IC-7200, TS-2000, and FTX-1 Optima rig profiles; CW keying hardening.
- ECHOCAT map pop-out to a browser window; iPad split-view support.
- **Logger32** added as a logbook forwarding target (April 25).

### v1.5.0 — April 2026 — "The SSTV Release"

- **SSTV** decoding: Martin M1 "on par with MMSSTV," with Scottie 1 close behind (first shipped in v1.4.8/1.4.9).
- **Mac, Linux, and Windows installers** built via GitHub Actions, downloadable at potacat.com.
- One-click **Report a Bug** (v1.5.1): redacted system snapshot, rig config, and log tail into a prefilled Discord post — grid square excluded.
- Milestone: roughly 6,000 downloads, 10,000 QSOs, and 102 versions in about 9 weeks.

### v1.4.x — April 2026

- **Desktop VFO dial with audio streaming on the PC**: knob, dialpad, mode selector, PTT, log button, operator heads-up display, and solar weather.
- **Multi-slice JTCAT for Flex** — monitor 4 or more slices at once.
- **WebSDR as an RX option** — SWL and HF-net listening, even for unlicensed users.
- **VFO Lock** and Elecraft K4/K4D rig profile (v1.4.2).

### v1.3.15 — April 2026

- **FreeDV on ECHOCAT** (bundled on Windows; Mac/Linux build the RADE decoder).
- **Voice Macros** — 5 slots, shared between phone and desktop, with auto-PTT.
- **Propagation Map** pop-out (RBN/PSKReporter, day/night overlay); GridTracker-style decode enrichment in JTCAT and ECHOCAT.
- ECHOCAT configurable, reorderable spot columns; TunerGenius 1x3 antenna switching.

### v1.3.11 — March 2026

- Native **ft8_lib decoder** replaces WASM — FT8 decoding 5–10x faster (~120 ms).
- Movable **S-Meter and SWR meter** on desktop and ECHOCAT.
- **K1EL WinKeyer (WK2/WK3)** keyer support and a floating, draggable **CW Macro** box with variables such as `{MYCALL}`, `{call}`, and `{op_firstname}`.
- **Keyboard CW** keying (VBand/Vail style: left `Ctrl` dit, right `Ctrl` dah, iambic timing).
- Activation **dupe detection** (DUPE tag and count badge); **Launcher** system tray icon on port `7301`.
- 10 Hz fine tuning on the ECHOCAT dial (v1.3.10).

### v1.2.2 — March 2026

- "Don't Cross the Streams": JTCAT FT8 decode fixed after crossed desktop audio streams.
- **MIDI remote CW** on ECHOCAT (Android only — iOS Safari blocks Web MIDI); local sidetone for CW macros.
- **Rig Model layer** decoupled from connection method, with unlimited **custom CAT commands** per rig.
- **Auto-chase** for POTA/SOTA/CQ spots; 4-row FT8 layout on ECHOCAT.

### v1.1.0 — March 2026 — "The FT8 + Remote CW Release"

- **Remote FT8** and **remote CW** on ECHOCAT; all CW/FT8 functionality rolled out free to everyone on March 19.
- **Watchlist band/mode filters** (v1.1.1): `K4SWL:20m`, `KI6NAZ:CW`, `W1AW:40m:SSB`.
- ECHOCAT **voice macros**, DTR keying for remote CW, and remote power on/off for Yaesu rigs.
- Electron 33→39 / Chromium 130→142 platform upgrade; docs.potacat.com link added in-app.

### v1.0.12 — March 2026

- **Rig Control Panel** (status-bar Rig button): ATU tune, noise blanker, power on/off, RF gain, TX power, and mode-aware filter width presets — unsupported controls auto-hide.
- Native **Icom CI-V serial** support (IC-7300/705/7610 and more) without Hamlib.
- **HF Nets & SWL Directory** ("Dir" tab, tap to tune) and Wake Lock on ECHOCAT (v1.0.16).
- ECHOCAT **Club Station Mode** beta (v1.0.8): callsign + password login with member badges.
- **MacLoggerDX** UDP forwarding on port `9090` (v1.0.7).

### v1.0 — March 9, 2026

- First stable release — "45 releases since launch."
- **Spacebar PTT** for ECHOCAT (iPad keyboards) and a cleaner Welcome screen.
- ECHOCAT audio settings in Quick Settings; new "Radio" filter for band/mode.

### ECHOCAT launch — March 4, 2026

- **ECHOCAT**: control the rig from a phone browser over a **Tailscale** VPN — 100% free.
- Requires Tailscale on the shack PC and phone; browse to `https://100.x.y.z:7300`.
- Per-rig RX/TX audio channels set in the Rig dropdown.
- Followed the same week by the **DX Terminal** cluster window with one-click QSY (v0.9.39) and **NG3K ADXO** DX-expedition spots (v0.9.40).

### v0.9.27 — March 2026

- **Activator Mode** (introduced in late-February rolling builds): activator log, RBN view of your own CQ pickups, and a sortable logbook with filtered ADIF export.
- Daily QSO **milestone celebrations** (10/25/50/100/150/200/250, with 500 as mega).
- WSJT-X auto-log now forwards to external logbooks; new Grid column; 2-fer double-logging fix.

### v0.9.22 — February 2026

- `F5` checks for a new version; **TCP rigctl** support.
- **DXCC tracker** by band and mode, built from your imported logbook.
- Event tracking: **WAS 250**, **CQ WW 160m**, and pre-loaded **13 Colonies**.
- POTA/DX pill column; QRZ request-flooding bugfix.

### v0.9.9 — February 2026

- **Auto-update** introduced — "the last version you have to download."
- Portable `.exe` still offered alongside the installer.

### v0.9.7 — February 2026

- **Serial CAT** using the Kenwood protocol, bypassing Hamlib (QRPLabs QMX/QDX and similar).
- **Worked Station Tracking**: green check, muted spots, auto-skip in scan, "Hide already-worked" — plus ADIF import (LoTW/QRZ) and POTA hunted-parks CSV import.
- **Light/dark theme** toggle and a continent filter (AF/AS/EU/NA/OC/SA).
- **Logbook forwarding** to N1MM+ (UDP `2333`), N3FJP (TCP `1100`), HRD (TCP `7826`), and Log4OM 2.
- **SmartSDR panadapter spots** (TCP `4992`); RBN watchlist spots in the main spot table.
- **POTA re-spot** feature included in the same build.

### v0.9.6 — February 2026

- **Ham Radio Deluxe** and **Log4OM 2** logging integrations go live.
- Pre-auto-update era: manual uninstall/reinstall required to upgrade.

---

For full release notes on every build, see the **#announcements** channel on the POTACAT Discord.
