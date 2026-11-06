# Icom IC-7300 & IC-7300 Mk II

The IC-7300 is one of the most popular rigs in the POTACAT community, and everything — CAT control, PTT, TX/RX audio, even remote CW keying — rides the radio's single built-in USB cable. The difference between rock-solid and flaky comes down to a handful of radio-side menu settings, so start here.

This page also covers the IC-7610, IC-7100, and IC-706MKIIG at the bottom.

## Quick setup

1. Add a new rig and select the **IC-7300** (or **IC-7300 Mk II**) profile.
2. Choose the radio's COM port (it enumerates as a Silicon Labs CP210x device on Windows).
3. Match the baud rate in POTACAT to the radio's **CI-V USB Baud Rate** — `19200` is the sweet spot (see below).
4. Set the rig's RX and TX audio devices in POTACAT to the radio's `USB Audio CODEC`. On Linux the same device may be listed under its chip name, such as `PCM2901` or `PCM2903B`.

## Radio-side CI-V settings

Open **MENU > SET > Connectors > CI-V** and set:

| Setting | Value | Why |
|---|---|---|
| CI-V Transceive | `OFF` | The big one. When ON, the radio's own status chatter collides with POTACAT's commands on the CI-V bus — the classic cause of PTT that only keys one try in three. |
| CI-V USB Baud Rate | `19200` (fixed) | See the trade-offs below. |
| CI-V USB Echo Back | `OFF` | With it ON, PTT gets intermittent and TX audio comes out thin with almost no ALC movement. |
| CI-V Address | `94h` (Mk II: `B6h`) | Must match the CI-V address in POTACAT's rig settings. |

> **Note:** Restart the radio after changing CI-V settings.

### Baud rate: fixed `19200` vs `Auto`

| You want | Set CI-V USB Baud Rate to |
|---|---|
| Reliable PTT and working FT8 decode in JTCAT | `19200`, fixed, matched on both the radio and POTACAT |
| CAT power-on from POTACAT/ECHOCAT | `Auto` |

- **Fixed `19200`** is the recommended setting: a fixed rate eliminates CI-V collisions, and JTCAT will not decode FT8 reliably with the radio at `115200`. Drop to `19200` on *both* sides.
- **`Auto`** is what makes the **Power On** button work. Waking a powered-down IC-7300 requires a long preamble of `FE` bytes before the CI-V power-on command — per Icom's manual, about 150 bytes at 115200 baud, 50 at 38400, 25 at 19200 — and with the radio on `Auto` this wake-up sequence has been confirmed to work. Power *off* works at any setting; power *on* is the hard part.

> **Note:** Powering the radio on from a full power-down is still a known rough edge — the radio takes several seconds to boot and the CAT connection can drop before it finishes. If Power On fails for you, keep the CI-V baud rate low (or `Auto`), or define a custom CAT power-on command: click **RIG** in the top bar, then **CAT**.

## Stuck in transmit after closing ECHOCAT

If the radio locks into TX when you close the ECHOCAT browser session, check **SET > Connectors > USB SEND/KEYING** and set **USB SEND** to `OFF`. When it's assigned to `RTS`, the serial control line can hold the radio keyed after the remote session ends. This is the durable, radio-side fix.

## Digital modes: MOD input and levels

- **SET > Connectors > MOD Input**: set **DATA MOD** to `USB` — some radios default data-mode audio to the ACC jack, which leaves JTCAT/FT8 transmitting dead air.
- **Voice silent but FT8 works?** Voice in plain USB/LSB uses **DATA OFF MOD**, a separate menu. Set **SET > Connectors > MOD Input > DATA OFF MOD** to `USB` (on an IC-7300 MK II too). See [Voice is silent, but FT8 works](ssb-over-data.md#voice-is-silent-but-ft8-works).
- **USB MOD Level** around 50% is a good starting point; watch the ALC meter during TX and back off if it's slamming.
- The radio's USB audio output must carry **AF** (normal receive audio), not IF — check the USB AF output setting under **SET > Connectors**.
- If ECHOCAT's RX meter shows clipping, lower the radio's USB AF output level — some users run it around 10%.

> **Tip:** For JTCAT, some users report good results with the RX slider around 37% and the radio's AF gain near the 10 o'clock position.

## Remote CW keying

Remote CW on the IC-7300 works well, but only over a **direct CI-V serial connection** — not through rigctld/Hamlib:

- On direct CI-V, POTACAT sends the radio's real CW key-down/key-up command (`0x1C 0x01`) for every paddle element.
- Hamlib's rigctld protocol has no per-element CW command — it only exposes the mic PTT line. Keying a paddle through rigctld raises PTT while the radio sits in CW mode: transmitter on, key line untouched, **silent TX**.

Setup:

1. Connect the rig as a direct CI-V serial rig (not rigctld Network / Hamlib).
2. On the radio, set **SET > Connectors > USB SEND/KEYING > USB Keying (CW)** to `USB(A) DTR`.
3. Leave POTACAT's **CW Key Port** set to `(none)` — the 7300 is keyed through its existing CI-V connection.

> **Warning:** **Linux users:** the kernel's `cdc-acm` driver can't control the DTR pin on the 7300's USB port (`Operation not supported` in the log). Worse, the stuck-high DTR line will key the radio continuously the moment it enters CW mode. On Linux, set **USB Keying (CW)** to `OFF` to stop the phantom keying. For real paddle keying, wire a cheap FTDI/CH340 USB-serial adapter to the radio's 3.5&nbsp;mm KEY jack (adapter DTR pin → tip, GND → sleeve) and select it as the **CW Key Port**. Note that common "CI-V data cables" are *not* keying cables — the DTR pin isn't broken out — and the CW Key Port must be a *different* COM port than your CAT port.

CW **text macros** are sent over the normal CAT connection and work everywhere, including Linux.

## FLRig as an alternative CAT path

CI-V serial drops commands that arrive nearly back-to-back; POTACAT compensates, but some IC-7300 owners find routing CAT through FLRig smoother — and the internal ATU can be triggered through FLRig, where POTACAT's direct ATU command doesn't work on this radio.

1. Run FLRig with its XML-RPC server on (the default, port `12345`).
2. In POTACAT, add the rig as **Other Rig (Hamlib)** with Rig Model **FLRig**, host `127.0.0.1`, port `12345`. FLRig owns the serial port — leave the COM/baud fields alone.
3. Alternatively, run your own bridge with `rigctld -m 4 -r 127.0.0.1:12345` and use the **rigctld Network** rig type.

## CI-V pacing: mode or power never reported

> **New in POTACAT 1.14.0.**

Some Icoms, the IC-7300 among them, drop a reply when POTACAT's next command arrives while they're still answering. On those radios the mode and RF power were never reported, which hid PTT and HALT and refused every Guest Pass transmission.

POTACAT starts every Icom exactly as before. If the radio answers the frequency but not the mode within about 10 seconds (or not its power while a Guest Pass needs it), POTACAT switches that radio to one command at a time and logs:

```
[CAT] This radio drops replies to back-to-back CI-V commands (...); sending them one at a time from now on.
```

That's normal, and the mode and power come back. It's checked again at each connect.

To set it yourself: **Settings > My Rigs**, edit the rig, **Advanced > CI-V pacing**:

| Choice | What it does |
|---|---|
| **Auto** (default) | One command at a time only if the radio drops replies |
| **Always one command at a time** | From the start of every connect |
| **Never** | Always send at full speed |

**Icom Network (RS-BA1)** connections are unchanged.

## Troubleshooting quick hits

- **Spot clicks stopped QSYing and the CAT badge is red** — make sure the **WSJT-X Mode** checkbox is off unless WSJT-X is actually running and configured.
- **Echo on ECHOCAT** — both the audio input *and* output must be the radio's `USB Audio CODEC`, never the PC's default mic/speakers.
- **Mode flips to USB-D on phone PTT** — that's the SSB-over-DATA feature. If you're operating with the radio's own mic, uncheck **SSB-over-DATA** in Settings.
- **No FT8 decodes** — CI-V baud at `19200` on both sides, and check the JTCAT RX slider.

## IC-7300 Mk II

- The Mk II's default CI-V address is **`B6h`**, not the original 7300's `94h`. This is the #1 Mk II gotcha — if you copied settings from an original 7300, fix the address and select the Mk II rig profile.
- The Mk II has a LAN port, and POTACAT can use it. See [IC-7300 Mk II over the network (LAN)](#ic-7300-mk-ii-over-the-network-lan) below. USB remains the most-proven connection.
- Everything else on this page (CI-V settings, USB SEND, CW keying, Linux notes) applies to the Mk II as well.

## IC-7300 Mk II over the network (LAN)

POTACAT speaks Icom's own network protocol (the one RS-BA1 uses) through its **Icom Network** connection. That carries CAT control and receive and transmit audio over your network, with no RS-BA1 and no USB cable. The IC-7300 Mk II, IC-705, IC-7610, IC-7760, IC-9700, IC-7851 and IC-R8600 can connect this way directly. The **original** IC-7300 has no LAN port; to reach one over the network, run wfview's wfserver on a computer next to it and connect to that.

Users have reported the Mk II working over Icom Network. It has had fewer reports than USB, and there have been reports of connection and transmit-audio problems, so if you can, get the radio working over USB first.

**On the radio:** turn on its network remote control in the radio's network settings and set up a network user name and password. Note the radio's IP address. See Icom's manual for the Mk II's network menu; we haven't documented its exact menu path here yet.

**In POTACAT:** add or edit the rig in **Settings > My Rigs** and choose:

| Field | Value |
|---|---|
| Connection type | **Icom Network (UDP / RS-BA1)** |
| Radio Model | **IC-7300 MK II** (CI-V address `B6h`) |
| Host / IP | The radio's IP address |
| Control port | `50001` (the default), unless you changed it on the radio |
| Civ port (optional) | Leave on auto |
| Username / Password | The network user you set up on the radio |
| Network TX gain | Start at the default and adjust while watching ALC |

Click **Test Connection**. For JTCAT and SSTV over the network, set **Audio source for JTCAT / SSTV** in the rig editor to the Icom Network audio option. Transmit level over the network is set with JTCAT's **Drive** and **TX Pwr**, **Network TX gain**, and the radio's LAN MOD level; aim for clean output with little or no ALC (see [Transmit Level](jtcat.md#transmit-level-tx-pwr-drive-and-alc)).

> **Tip:** At the radio's factory setting, audio from the network reaches the transmitter only in DATA mode, so POTACAT switches to USB-D for each voice transmission. If you set the radio's **DATA OFF MOD** menu to **LAN**, tick **Voice over the LAN stays in USB / LSB** in the rig editor: voice then goes out in plain USB or LSB, with the radio's speech compressor and SSB filter.

## IC-7610

- CI-V address is **`98h`**.
- **No TX audio from ECHOCAT/digital modes**: set **MENU > SET > Connectors > MOD INPUT > SSB MOD** to `USB1` (or `USB2`, whichever port your cable is on), and set **SSB-D MOD** to the same.
- If **Test Connection** passes but the radio never QSYs, type the bare COM port name (e.g. `COM7`) into the manual COM field instead of accepting the auto-detected "Silicon Labs CP210x" dropdown entry.

## IC-7100 & IC-706MKIIG (DigiRig)

The same CI-V hygiene applies — **CI-V Transceive `OFF`** and a fixed baud rate cure most flakiness on the IC-7100 too.

The IC-706MKIIG (CI-V address `58h`) has a firmware quirk: it accepts CAT PTT but doesn't route TX audio to the rear interface, so PTT must be keyed on the DigiRig's hardware PTT line instead:

- Set the **PTT Port** field in the rig's Hamlib settings (**Settings > Rig**).
- **Two-port DigiRig**: CAT on one COM port, PTT Port on the *other* COM port.
- **DigiRig Mobile (single port)**: CAT and PTT share one COM port — use the DTR/RTS pin selector (default `DTR`; some units key on `RTS`).
