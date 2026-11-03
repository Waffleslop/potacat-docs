# JTCAT (Built-in FT8 & FT4)

JTCAT is POTACAT's built-in digital-modes engine. It decodes and transmits FT8, FT4, and FT2 entirely on its own — **you do not need WSJT-X installed**. JTCAT runs as a pop-out window on the desktop, and the same engine powers the FT8 screen in ECHOCAT on your phone.

While it runs, JTCAT:

- Decodes your radio's USB audio and shows decodes on a waterfall
- QSYs the radio and switches it into its data mode automatically
- Auto-replies to callers and can run Auto-CQ / Auto-POTA sequences
- Auto-logs completed QSOs and forwards them to your configured logbooks
- Reports decodes to PSKReporter

> **Note:** JTCAT takes over radio control while it is running — POTACAT's normal CAT connection is suspended until you stop it.

## JTCAT vs. WSJT-X vs. ECHOCAT

These three names get mixed up constantly. Here's the map:

| Name | What it is | When you use it |
|------|------------|-----------------|
| **JTCAT** | POTACAT's built-in FT8/FT4 engine (desktop pop-out window) | You want FT8 with nothing else installed |
| **WSJT-X** | A separate application; POTACAT can interoperate with it over UDP | You prefer WSJT-X for decoding/TX and want POTACAT to highlight POTA activators and log |
| **ECHOCAT** | POTACAT's phone/tablet remote control; its FT8 screen is a remote view of the JTCAT engine on your desktop | You want to work FT8 from the couch or away from the shack |

> **Warning:** To use JTCAT, the **WSJT-X** mode checkbox under the **CAT** pill must be **unchecked**. WSJT-X Mode hands rig control to an external WSJT-X and disables POTACAT's own CAT — JTCAT cannot run in that state. See the [WSJT-X](wsjt-x.md) page for how that mode works.

## Audio Setup

JTCAT listens to — and transmits through — your radio's USB audio codec. Audio devices are configured **per rig** under **Settings → Radio → Edit**:

- **Audio input (RX):** the radio's USB audio device, selected explicitly (for example `USB Audio CODEC` for an IC-7300, or `FT-710 USB Audio`). Don't leave it on "Default" unless the radio genuinely is your operating system's default recording device.
- **Audio output (TX):** the same radio USB device, so TX audio reaches the rig instead of your computer speakers.

> **Tip:** The classic symptom of a wrong input device: the waterfall reacts to the radio's speaker volume knob or to room noise. That means JTCAT is listening to a microphone, not the rig.

Platform and rig specifics:

- **macOS** — grant Microphone permission to POTACAT in **System Settings → Privacy & Security → Microphone**. Without it, decoding silently fails; the log shows `Cycle boundary: ... max=0.0000`.
- **FlexRadio** — use the **Flex Direct (VITA-49)** audio source; no DAX program is needed. PTT requires the **SmartSDR API host (port 4992)** configured in the rig settings — this is separate from the SmartCAT connection.
- **Rigs without built-in USB audio** (for example the Xiegu G90) — use an external USB sound-card interface.

## Radio Mode (DATA) Setup

The rig must be in its data mode — USB-D on Icom, DATA-USB on Yaesu, DIGU on Kenwood, DATA A on Elecraft. JTCAT sets and enforces this automatically (the log shows `post-reconnect mode enforcement: FT8`), but a few radios need extra attention:

- **Yaesu** — the data mode is labeled DATA on most models and PKT on some older ones; either way, make sure data-mode audio comes from the rear/USB input (**DATA MOD = USB** — some rigs default it to the ACC jack).
- **Yaesu FTDX10 / FTDX101 family** — in DATA mode these rigs can transmit offset from the dial by the carrier point (roughly 600 Hz) with a narrowed filter. Set **MENU → OPERATION SETTING → GENERAL → DATA MODE** to `Others` (or `DATA-STD`, depending on firmware) so TX lands where the dial says.
- **Elecraft KX2/KX3** — per-band memory recall can override DATA A on a band change. Select **KX2/KX3** as the Radio Model in **Settings → Radio** so POTACAT re-sends the mode after each QSY.

## Clock Sync

FT8 lives and dies by your computer clock — an offset of even a few seconds kills decoding entirely. JTCAT shows a **clock-sync banner** when your system clock is off; if you see it, sync your clock to internet time before troubleshooting anything else.

The JTCAT panel also has a **Latency (ms)** control — the equivalent of WSJT-X's "Audio: Soundcard time delay." It is auto-calibrated, so you normally never touch it, but if your DT readings look consistently offset it's the knob to check.

## Making QSOs

Click a decode (or a highlighted POTA activator) to reply. JTCAT runs the exchange — reports, RR73, 73 — automatically.

- **Late-join TX** — you don't have to wait for the top of a cycle. Click partway into a TX window and JTCAT starts a shortened reply immediately, matching WSJT-X's late transmit start.
- **AP decoding** — a-priori decoding is supported, which helps pull out weak replies directed at you.
- **Hold TX** — this checkbox is the equivalent of WSJT-X's "Hold Tx Freq": your transmit frequency stays pinned to the value in the TX Freq box while RX follows the other station. The setting persists between sessions.
- **TX slot lock** (from 1.13.3) — the **Slot** menu offers **Auto**, **1st (even)** or **2nd (odd)**, for FT8, FT4 and FT2. Locked, every CQ and reply stays in that slot, and JTCAT won't call a station transmitting in your slot; clicking one offers **Unlock and call**. Hound mode ignores the lock. On **Auto**, your CQ stays in the slot you last transmitted in for 30 minutes. ECHOCAT Web has the same **Slot** button.
- **dB numbers are confidence scores** — JTCAT's per-decode signal figures are the decoder's own confidence score, **not** calibrated SNR. Don't expect them to match WSJT-X's dB readings.

### Send your own message

To transmit something other than the next step of the exchange, **click the TX message readout** (the line showing the message that will be transmitted) and type. Press **Enter** to accept it or **Esc** to cancel.

- You can type a standard message (for example `K1ABC W9XYZ R-12`) or **free text of up to 13 characters**, using `A-Z`, `0-9`, space and `+ - . / ?`. POTACAT checks it before accepting it.
- Typing a message doesn't start transmitting; enable TX as usual.
- It's sent once in place of the current step. When the QSO moves on, the next step replaces it.
- You can also click the highlighted step in the QSO tracker to edit it.

On the phone, a directed CQ such as `CQ POTA` is set with **FT8 → Target → Custom** in ECHOCAT (see [below](#ft8-on-your-phone-echocat)).

## Transmit Level: TX Pwr, Drive and ALC

The audio bar in the JTCAT window has two transmit controls that do different jobs:

- **TX Pwr** sets the radio's **RF output power**, in watts, over CAT.
- **Drive** sets the **audio level** POTACAT sends into the radio. It controls modulation, not power. The scale is logarithmic, so you get fine control at the low end. (On a Flex connected with Flex Direct, audio goes at full scale and Drive is dimmed.)

**ALC** is the radio's automatic level control. It moves when the audio going in is more than the transmitter needs. For FT8 and the other digital modes you want clean audio, so set Drive (and the radio's USB or data MOD level) so the ALC shows **little or no movement** while the radio still reaches the power set by TX Pwr. Lots of ALC means the signal is being compressed and splatters. No ALC at all is fine on some radios (Elecraft, for example) as long as the power comes up.

Where to see ALC: the radio's own meter, the **ALC·TX** meter in POTACAT's rig panel, the meters in the VFO window, or ECHOCAT Web. The radio reports ALC only while transmitting. The JTCAT window shows S, PWR and SWR, not ALC.

To set it up: key a transmission into a dummy load or a clear frequency, start with Drive low, and raise it until the power reaches TX Pwr; back off if ALC climbs. If power stays near zero whatever Drive says, the radio isn't taking audio from USB. See [Radio transmits but nothing shows on PSKReporter](#radio-transmits-but-nothing-shows-on-pskreporter).

> **Tip:** The [SSTV](sstv.md) window has its own **Drive** slider, set separately from JTCAT's.

## Use GridTracker with JTCAT

GridTracker can show JTCAT's decodes and start QSOs in JTCAT, as it does with WSJT-X. From POTACAT 1.13.6:

1. Open **Settings > Logging** and turn on **Also broadcast each QSO to an extra UDP port**.
2. Set the host to `127.0.0.1` (GridTracker on the same PC), the port to GridTracker's, normally **2237**, and the format to **WSJT-X binary (GridTracker, JTAlert, HamRS)**.
3. Leave **Send FT8/FT4 decodes too, and answer the station I double-click in GridTracker** ticked (it is on by default).

GridTracker's call roster then fills from the JTCAT window, a double-click on a station in GridTracker answers it in JTCAT, just like a double-click in the decode list, and each logged QSO is sent to GridTracker. See also [Logbook Forwarding: GridTracker](logbook-forwarding.md#gridtracker).

## JTTY

JTTY (the WSJT-X 3.2 keyboard mode: 4-GFSK, 127 Hz wide, no timed sequences) has its own pane in the JTCAT window. From POTACAT 1.13.0:

- **Chats.** The tab strip above the decodes holds all traffic plus one tab per station. Double-click a line to open a chat with that station and see the exchange as a conversation; the composer has the pair of callsigns filled in. A station calling you opens a tab without switching you away from the one you are in. Right-click a tab for **Log** (log the QSO) and **Close**. Chats work with **Style** set to **FT8**.
- **CQ on a clear spot.** When you call CQ, JTCAT first moves to the quietest spot near your offset, measured over the last 30 seconds of the passband, so a fresh session no longer calls on 1500 Hz with everyone else. **Clear spot** does the same on demand. Turn on **Hold** (Hold TX frequency) to stay where you are. The move is made on the shack, so a CQ from the phone or a [paired laptop](remote-desktop.md) gets it too.

## WSPR Map

From 1.13.3, the WSPR map in the JTCAT window has a legend for its colours: **green** for -10 dB or better, **amber** for -11 to -20 dB, **red** below -20 dB, and **grey** for no report.

## Auto-Logging

JTCAT logs each QSO automatically when the report exchange completes and forwards it to any logbooks you've configured — see [Logbook Forwarding](logbook-forwarding.md). There's nothing to click.

From 1.13.3, a contact made with no frequency from the radio (CAT not connected) is logged on the band's FT8 dial frequency, so Wavelog and other logbooks don't refuse it as 0 kHz.

That includes interrupted endings: if you click a new station while the previous QSO is still in its 73/courtesy phase, the completed QSO is logged **before** the new one replaces it.

> **Note:** Some users report a logging bug where a QSO is logged immediately after the report is sent, with the sent RST recorded as both sent *and* received. If your logged reports look mirrored, check and correct the entry in the logbook.

## Troubleshooting

If nothing here fixes it, see [Report a Bug](../community--support.md#report-a-bug).

### Nothing decodes

Work through these in order:

1. **Audio input device** — must be the radio's USB codec, not "Default" or a microphone. See [Audio Setup](#audio-setup).
2. **macOS Microphone permission** — **System Settings → Privacy & Security → Microphone**.
3. **RX gain** — too high (clipping) or too low both kill decodes. If the RX meter shows a red CLIP indicator, lower the rig's USB audio output level (or the OS recording level) rather than only the app slider; some IC-7300 users report running the rig's USB output level as low as about 10%.
4. **Clock offset** — look for the clock-sync banner and sync your system clock.

### Radio transmits but nothing shows on PSKReporter

The five-step checklist:

1. **Watch the ALC meter during TX.** Zero deflection means audio isn't reaching the modulator at all.
2. **IC-7300:** set **MENU → SET → Connectors → USB MOD Level** to about 50%.
3. **DATA MOD = USB** — some rigs default data-mode audio to the ACC jack.
4. **Drive** in the JTCAT window (or ECHOCAT) is not at 0. See [Transmit Level](#transmit-level-tx-pwr-drive-and-alc).
5. **Cross-check with WSJT-X** on the same audio devices to separate an app problem from a radio configuration problem.

### Waterfall quirks

- A waterfall that follows the radio's volume knob or room noise means the wrong audio input device is selected.
- Some users report the phone (ECHOCAT) waterfall not displaying even while decodes flow — decoding happens on the desktop, so QSOs still work.
- If decodes or the waterfall stall after a long or resumed session, restart POTACAT (or close and reopen the JTCAT window). Newer builds include a watchdog that restarts audio capture automatically after several silent cycles.

### Running from source

Packaged builds ship with the fast native C decoder (`ft8_lib`). If you run POTACAT from source on macOS, install the Xcode command-line tools (`xcode-select --install`) and run `npm run build-ft8`; otherwise JTCAT falls back to a slower WASM decoder. The terminal shows which one loaded: `[FT8 Worker] Native C decoder loaded (ft8_lib)` versus `Native decoder not available, using WASM fallback`.

## FT8 on Your Phone (ECHOCAT)

ECHOCAT's FT8 screen drives the same JTCAT engine on your desktop, so everything above still applies — configure audio and rig mode on the desktop first.

One behavior trips up WSJT-X veterans: an FT8 transmission needs about 12.5 seconds of the 15-second window, so **you have roughly a 2-second grace window at the start of a TX cycle to tap a reply**. Tap within it and the reply goes out immediately (late-join TX may still squeeze in a shortened reply if you're slightly late); miss it and JTCAT waits for the next cycle. This is FT8 timing physics, not a bug.

> **Note:** ECHOCAT is a remote control — every tap travels to your desktop before anything happens. The latency figure at the top of the app shows that round trip; the higher it is, the less of the grace window you have.

Two more phone-side pointers:

- In FT8 mode, the PTT/transmit controls live inside the **FT8 banner**. Press **Stop** there before switching back to the Spots or VFO views.
- To call a directed CQ (such as `CQ POTA`), set **FT8 → Target → Custom** in ECHOCAT.
