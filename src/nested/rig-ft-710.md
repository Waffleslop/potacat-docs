# Yaesu FT-710

**Best for:** Yaesu FT-710 (AESS / Field) — CAT, audio, and remote CW all over the radio's single USB cable.

The FT-710 exposes **two COM ports and a USB sound card** over one USB cable. The **Enhanced** COM port is the one that carries CAT — use it for the rig connection. For general connection-method background, see [Radio Setup](../radio-setup.md).

## Connection settings

1. **Windows:** install the **Silicon Labs CP210x USB-to-UART driver** before you plug in the radio. Without it, no COM port appears. It's on the Files tab of the FT-710's page on Yaesu's website, or Silicon Labs' "CP210x USB to UART Bridge VCP Drivers" page. (The separate "virtual sound driver" is not needed.) **Linux:** no driver needed; the radio is plug-and-play.
2. Add a new rig → select **Serial CAT (Kenwood / Yaesu)** ([details](serial-cat-kenwood.md)) — not Hamlib.
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
| **RADIO SETTING → MODE SSB → SSB MOD SOURCE** | `REAR` | Without this, remote voice keys the radio but nothing is modulated (0 W, no ALC), even though FT8 works |
| **RADIO SETTING → MODE SSB → REAR SELECT** | `USB` | Takes the rear-port voice audio from the USB sound card |
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

## Band scope (LibFT4222)

On Windows, POTACAT reads the FT-710's band scope through FTDI's **LibFT4222** library. It's FTDI's own closed-source library, so POTACAT can't include it; you download it once from FTDI.

1. Open **Settings > Station Setup**. The band scope step opens FTDI's download page for LibFT4222.
2. Download and unzip it, then press **Find the file for me**. POTACAT copies the library into place. Pick the 64-bit file (`LibFT4222-64.dll` in the `amd64` folder); a 32-bit copy doesn't count as installed.
3. Reopen the Band Scope.

If the scope still says the library isn't installed, or that the FTDI driver couldn't be loaded:

- In Windows **Device Manager**, find the FT4222 device, uninstall it (tick the box to delete its driver if offered), unplug and replug the radio, and let the driver install again.
- If the message names the **D2XX** driver, install FTDI's D2XX driver from ftdichip.com and reopen the Band Scope.

## Known quirks

- **ATU:** remote tune via CAT is not supported by Yaesu's firmware on this radio — no CAT command starts a tune cycle. Use the front-panel **TUNE** button.
- **SWR bar:** before 1.13.1, POTACAT read the ALC meter as SWR on Yaesu rigs, so a perfect match could show 3:1. From 1.13.1 it reads the real SWR meter, scaled the way Hamlib and WSJT-X scale it.
- Some users report that a few panel controls (ATT, preamp, COMP, NR, ANF, VOX) don't respond from POTACAT even though the power slider, VFO knob, and power on/off work fine.
