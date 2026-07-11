# Yaesu FTDX10 & FTDX3000

**Best for:** Yaesu FTDX10, FTDX3000, and FTDX101D/MP — with notes for the FT-991A.

These rigs share the same Yaesu CAT protocol and the same remote-audio menu family, but each has its own gotchas. For connection-method background, see [Radio Setup](../radio-setup.md).

## Connection settings

All of these radios work well as **Serial CAT (Kenwood)** ([details](serial-cat-kenwood.md)) at `38400` baud.

**FTDX3000** — if the frequency won't change, check these radio menus:

| Menu | Set to |
|------|--------|
| **MENU 037 CAT SELECT** | `USB` |
| **MENU 038 CAT RATE** | match POTACAT (`38400` works) |
| **MENU 040 CAT RTS** | `ENABLE` |

With **CAT RTS = ENABLE**, leave **Disable DTR/RTS on connect** *unchecked* in POTACAT — the wrong combination of the two is the classic "CAT connects but frequency won't change" cause on this rig.

**FTDX101D/MP** — the radio exposes two virtual COM ports (Enhanced and Standard). To share the radio with a logger, enable CAT on both USB ports in the radio menu and point POTACAT at the port the logger isn't using. Prefer the Serial CAT rig type over Hamlib on the 101 — it's the stable path for CW macros.

## Radio menu settings

### FTDX10

| Menu | Set to | Why |
|------|--------|-----|
| **RADIO SETTING → MODE SSB → SSB MOD SOURCE** | `REAR` | Without it, remote PTT keys the radio but no audio transmits (the mic still works normally — mic PTT re-selects the mic) |
| **RADIO SETTING → MODE SSB → REAR SELECT** | `USB` | Takes rear-port TX audio from the USB sound card |
| **OPERATION SETTING → GENERAL → DATA MODE** | `Others` / `DATA-STD` (label varies by firmware) | In `PSK` mode the TX lands off the dial frequency in DATA modes |

### FTDX3000

| Menu | Set to | Why |
|------|--------|-----|
| **MENU 103** | `USB` | Routes SSB TX audio from the USB port for ECHOCAT (switch it back for front-mic use) |

### FTDX101D / FTDX101MP

| Menu | Set to | Why |
|------|--------|-----|
| **MODE SSB → SSB MOD SOURCE** | `REAR` | Options are `MIC`/`REAR` on the 101 family — there is no `AUTO` |
| **REAR SELECT** | `USB` | TX audio from the USB sound card |
| **RPORT GAIN** | start around `1` | `50` is far too hot and distorts badly — start at 1 and work up |
| **DATA MODE** | `Others` (not `PSK`) | In `PSK` mode the radio shifts TX ~1.5 kHz below the dial |

> **Note:** On Yaesu rigs the shack mic can stay live during remote SSB transmit — there's no CAT command to mute it. With **SSB MOD SOURCE = REAR** the mic only transmits via its own PTT; otherwise turn the mic down or unplug it when operating remote, or use [SSB over DATA](ssb-over-data.md).

## CW keying

- Yaesu CAT ports handle **CW text macros** (the `KY` command) but not real-time paddle keying. For a paddle, wire a cheap FTDI/CH340 USB-serial adapter to the radio's **CW KEY jack** and select it as the **CW Key Port** in POTACAT Settings — it keys per-element via DTR pulses regardless of CAT backend.
- **Exception — FTDX101D:** paddle keying works over plain CAT (`TX1;`/`TX0;`) with no adapter needed.
- **FTDX3000:** the **CW Key Port** must be the radio's *Standard* COM port — never the same port as CAT. Pointing both at one port causes an endless connect/disconnect loop. Leave **CW Key Port** blank unless you have a second port or dedicated keying adapter.
- Over Hamlib/rigctld there is no per-element CW command at all — POTACAT disables the paddle with a red banner unless a **CW Key Port** is set. Another reason to prefer Serial CAT.
- Make sure break-in (**BK-IN**) is on, or the radio queues CW without transmitting. Some users report the FTDX10 remembers BK-IN *per band* — if CW sidetones but produces no RF, check BK-IN on the current band.

## Audio & digital modes

- **SSB-over-DATA breaks the FTDX10**: with it enabled, PTT drops the rig into DATA-L with a ~650 Hz offset and a 600 Hz filter. Uncheck **Settings → ECHOCAT → SSB-over-DATA** on this rig, and use the `REAR`/`USB` menu settings above for remote audio instead. See [SSB over DATA](ssb-over-data.md).
- The same applies to the **FTDX3000**: uncheck SSB-over-DATA and set **MENU 103** to `USB`.
- **2.4 kHz DATA filter limit (FTDX3000/FTDX5000):** DATA-U/PKT modes max out at 2.4 kHz IF bandwidth — too narrow for FreeDV and marginal for FT8, while plain USB allows 4 kHz. POTACAT's JTCAT uses plain USB on these rigs; for FreeDV, set **Settings → Spots → FreeDV sideband** to `Always upper` and leave **Switch radio to DATA mode** unchecked.
- **SWR/ALC meters are transmit-only** — during RX the bars stay at `—` by design. Key into a dummy load to verify them.

> **Tip:** If your filter width snaps back to the app default (2300 Hz) on every QSY, set your per-mode default filters in **Settings → Tuning** — they persist after that.

## FT-991A notes

- Set **MENU 109 SSB PORT SELECT** so SSB TX audio comes from the USB port (`USB`) — required for ECHOCAT voice.
- Like the FT-710, change the radio's **DATA MODE** from `PSK` to `OTHERS` if you use SSB-over-DATA, or TX lands off frequency.
- **Sharing the radio with Win4Yaesu:** Win4Yaesu holds the physical CAT port, so bridge POTACAT through a com0com virtual port pair with rig type **Serial CAT (Kenwood)** — see [Win4Yaesu Setup](win4yaesu-setup.md). Note that com0com does not work inside a Windows VM; VSP Manager (free for hams) is an alternative there.

> **Warning:** The FT-991A's `KY` command has no free-text form, so **CW text macros key the transmitter but produce zero RF** — same known open limitation as the FT-891. Use a DTR keying adapter on the key jack for working remote CW.

## Known quirks

- **FTDX10:** stay on VFO A — some users report misbehavior when the rig is left on VFO B.
- **FTDX10:** the mode names are DATA-L/DATA-U/DATA-FM only — there is no "DATA-STD" *mode* (the similarly named option belongs to the **DATA MODE** menu setting above).
