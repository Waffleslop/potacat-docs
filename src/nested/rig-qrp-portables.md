# QRP & Portable Rigs

Setup notes for the small rigs the community runs POTACAT with in the field — Xiegu, QRP Labs, (tru)SDX, and sBitx.

## Xiegu G90

- **Baud rate is the classic G90 failure.** The G90's factory CAT baud is **`19200`**; if POTACAT is left at the default `9600`, the radio just silently ignores everything. Set `19200` in the rig settings.
- Connect as **Other Rig (Hamlib)** at `19200`. If the G90 profile won't read the frequency, some users have success selecting the **X5105** (or IC-718) model instead.
- **ATU**: the G90's CAT protocol has no working remote-tune command — use the front-panel tuner button. This is a radio limitation, not a POTACAT one.
- The TX power slider is a **percentage of maximum power, not watts** — `50` on a 20&nbsp;W radio means 10&nbsp;W. (True for every rig, but most noticeable on QRP radios.)
- **ECHOCAT audio**: the G90 only passes USB audio in **U-D (data) mode**, but in data mode ECHOCAT hides the SSB PTT button (PTT is shown for SSB/FreeDV only) and you can't switch modes back from the phone. Plan your mode before you walk away from the radio. Audio interfaces in community use: Xiegu CE-19, DE-19, and xggcomms units.

## Xiegu X6100 / X6200

- **X6100 on a Raspberry Pi**: the proven path is bridging through FLRig. Run `rigctld -m 4 -r 127.0.0.1:12345` (Hamlib model 4 = FLRig), then set the POTACAT rig type to **rigctld Network** at `127.0.0.1:4532`. Pointing Hamlib directly at the X6100's serial port at 19200 has been slow or failed to QSY for some users.
- **X6200**: if ECHOCAT's FT8 view decodes but desktop JTCAT shows no band activity, turn up the **RX level slider** in JTCAT — the input level defaults too low for this radio.

## QRP Labs QMX / QMX+

- Connect as **Serial CAT (Kenwood)** on the QMX's *first* USB serial port at `38400` baud — don't use Hamlib. If the QMX gets stuck in terminal mode, power-cycle it.
- Set the **Radio Model** dropdown to **QMX** — it's separate from the connection settings, and the QMX-specific behavior only applies when the model is selected.

### Remote CW keying

Remote CW on the QMX requires **firmware 1.03 (`1_003_0`) or later** for DTR keying on the second USB port. The confirmed working recipe:

| Where | Setting |
|---|---|
| QMX menu **System > GPS & Ser.Ports** | Serial Ports = `2` |
| QMX menu **CW > CW Keyer** | Key from USB DTR = `USB 2` |
| POTACAT rig | Serial CAT (Kenwood), QMX port 1, `38400`, **Disable DTR/RTS on connect** checked |
| POTACAT audio in/out | QMX Digital Audio Interface |
| **CW Key Port (DTR keying)** | The QMX's **second** COM port |

> **Warning:** On Linux, the kernel's `cdc-acm` driver can't toggle DTR on the QMX's USB ports, so real-time paddle keying fails with `Operation not supported`. Use an external FTDI/CH340 USB-serial adapter into the key jack as the CW Key Port, or stick to CW **text macros**, which go over the normal CAT connection and work fine.

Other QMX notes:

- Linux: if saving the rig fails with "Cannot lock port", you can hand-edit `~/.config/potacat/settings.json` — give the rig `type: serial-cat`, `port: /dev/ttyACM0`, `baudRate: 38400`, `disableDtrRts: true`.
- Very faint phone audio through ECHOCAT is usually the radio-side output level — turn it up on the QMX.

## (tru)SDX

- Works out of the box as **Serial CAT (Kenwood)** at **`115200`** baud.
- Power expectations: roughly 0.5&nbsp;W on USB power alone, about 5&nbsp;W on a 12&nbsp;V supply.

## sBitx and other ALSA-only Linux radios

POTACAT is a Chromium-based app, so its audio dropdowns show only devices that **PulseAudio/PipeWire** publishes — raw ALSA `hw:`/`plughw:` devices are invisible by design. The sBitx image disables PulseAudio entirely, which hides the radio's loopback devices from POTACAT.

The fix is to re-enable the sound server and publish the loopbacks as named devices:

1. Re-enable PulseAudio (comment out `autospawn = no` in `/etc/pulse/client.conf`) or install PipeWire: `sudo apt install pipewire pipewire-pulse wireplumber`
2. Publish the RX loopback: `pactl load-module module-alsa-source device=hw:1,1 source_name=sbitx_rx`
3. Publish the TX loopback: `pactl load-module module-alsa-sink device=hw:2,0 sink_name=sbitx_tx`
4. Persist the `load-module` lines in `/etc/pulse/default.pa` so they survive a reboot.

The named `sbitx_rx`/`sbitx_tx` devices then appear in POTACAT's audio dropdowns. The same pattern works for any Linux SDR that only exposes ALSA devices.
