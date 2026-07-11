# Yaesu FT-710

**Best for:** Yaesu FT-710 (AESS / Field) — CAT, audio, and remote CW all over the radio's single USB cable.

The FT-710 exposes **two COM ports and a USB sound card** over one USB cable. The **Enhanced** COM port is the one that carries CAT — use it for the rig connection. For general connection-method background, see [Radio Setup](../radio-setup.md).

## Connection settings

1. **Windows:** install Yaesu's FT-710 USB driver from their website (the plain USB driver — the separate "virtual sound driver" is not needed). **Linux:** no driver needed; the radio is plug-and-play.
2. Add a new rig → select **Serial CAT (Kenwood)** ([details](serial-cat-kenwood.md)) — not Hamlib.
3. Choose the radio's **Enhanced** COM port.
4. Set the baud rate to `38400` (matching the radio's CAT rate).
5. Check **Disable DTR/RTS on connect**.
6. Click **Test Connection**, then Save.

> **Note:** Use Serial CAT rather than **Other Rig (Hamlib)** for this radio. Under Hamlib, power-on and several rig-control buttons are unreliable on the FT-710. Over Serial CAT, remote **power on/off works** — including from the ECHOCAT power button.

> **Tip:** Power the radio on before opening the rig settings screen — with the radio off, the audio device dropdowns stay empty.

## Radio menu settings

| Menu | Set to | Why |
|------|--------|-----|
| **OPERATION SETTING → GENERAL → CAT-1 TIME OUT TIMER** | `1000` ms | The factory default of 10 ms is too short for CAT round-trips and causes spurious `?;` command rejections |
| **RADIO SETTING → MODE SSB → MOD SOURCE** | `AUTO` | Without this, remote PTT keys the radio but nothing is modulated |
| **OPERATION SETTING → CAT/LINEAR/TUNER → USB KEYING (CW)** | `DTR` | Required for remote CW keying (see below) |
| **FUNC → RADIO SETTING → CW → CW BK-IN** | `ON` (or `SEMI`) | Without break-in the radio queues CW text but never keys the transmitter |

## Audio & digital modes

- In Windows **Sound settings**, set the radio's USB audio device to **16 bit, 44100 Hz (CD Quality)**. The Windows default of 48000 Hz breaks TX audio on this radio.
- In POTACAT's rig settings, set **RX Audio In** and **TX Audio Out** both to the radio's USB audio codec. A common failure is TX audio routed to the PC speakers instead of the rig.
- **SSB-over-DATA** (Settings → ECHOCAT) works well on the FT-710. The radio flipping to **DATA-U** in red while you key from the phone is normal and expected — see [SSB over DATA](ssb-over-data.md).
- If you use SSB-over-DATA, also change the radio's **DATA MODE** setting from `PSK` to `OTHERS` — otherwise TX lands off the dial frequency in DATA mode.

## CW keying

The FT-710's CAT `KY` command is unreliable for CW text — it raises the carrier but doesn't reliably key Morse. POTACAT instead keys this radio per-element using **DTR on the radio's second (CAT-2) COM port**:

1. In POTACAT Settings, set **CW Key Port** to the radio's second COM port (e.g. `COM4` if CAT is on `COM3`, or `/dev/ttyUSB1` on Linux).
2. On the radio, set **OPERATION SETTING → CAT/LINEAR/TUNER → USB KEYING (CW)** to `DTR`.
3. Turn break-in on: **FUNC → RADIO SETTING → CW → CW BK-IN** = `ON` or `SEMI`.

Without a **CW Key Port** configured, POTACAT falls back to the `KY` command — expect missed or garbled sending.

> **Warning:** On Linux, some `cdc_acm` USB-serial drivers can't control the DTR pin (`Operation not supported` in the log). The pin sticks high and the radio can key continuously while POTACAT runs. POTACAT falls back to a Python/pyserial helper for CW text (install `python3` and `pyserial`), but that only handles word-at-a-time text — real-time paddle keying needs a cheap FTDI/CH340 USB-serial adapter wired to the rear **KEY** jack, set as the **CW Key Port**. If the rig gets stuck keyed, set **USB KEYING (CW)** = `OFF` on the radio.

## Known quirks

- **ATU:** remote tune via CAT is not supported by Yaesu's firmware on this radio — no CAT command starts a tune cycle. Use the front-panel **TUNE** button.
- **SWR bar:** POTACAT's SWR bar over-reads on Yaesu rigs — trust the radio's own meter.
- Some users report that a few panel controls (ATT, preamp, COMP, NR, ANF, VOX) don't respond from POTACAT even though the power slider, VFO knob, and power on/off work fine.
