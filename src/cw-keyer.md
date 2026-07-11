# CW Keyer

POTACAT includes a built-in CW keyer. Plug in a MIDI paddle (e.g. HaliKey or N6ARA TinyMIDI), a keyboard-emulating adapter (VBand or Vail), or a K1EL WinKeyer, and POTACAT keys your radio — no separate keyer software required. You can also send CW without any key at all, using the text box and macro buttons.

**Setup:**
1. Enable CW Keyer in **Settings > CW Keyer**
2. Select your **Keyer Mode**: Iambic B, Iambic A, or Straight key
3. Set your **Speed** (WPM)
4. Click **Refresh** to detect MIDI devices, then select yours
5. Use the **Learn** buttons to map dit and dah MIDI notes from your paddle
6. Enable **Local sidetone** and adjust pitch/volume

**How it works:** POTACAT reads your paddle events (MIDI via the Web MIDI API, or Ctrl-key presses from a VBand/Vail adapter), runs an Iambic keyer state machine, and keys the radio over the best route available for your rig — `cw key` commands via the SmartSDR TCP API on FlexRadio, CI-V key up/down commands on Icom, or DTR pulses on a dedicated serial port. This preserves your exact fist timing — no buffering.

**CW status:** The CW pill in the status bar shows keyer state. Click it for a popover with volume and WPM controls. The sidetone requires one click anywhere in the app to unlock (browser audio policy).

## WinKeyer

The K1EL WinKeyer (WK2/WK3) is supported as a keyer type. Select it in **Settings > CW Keyer** and choose its serial port in the **WinKeyer Port** dropdown. WinKeyer also works with FlexRadio direct connections — you can key a Flex through a WinKeyer on the PC without SmartSDR running.

> **Tip:** If your WinKeyer (or a virtual COM port) doesn't appear in the dropdown, type the port name manually (e.g. `COM5`). The **WinKeyer Port** and **CW Key Port** fields both accept typed port names in addition to the auto-detected list.

> **Note:** Some left-handed operators report that POTACAT sets the WinKeyer to its normal (non-swapped) paddle mode, and there is currently no in-app paddle-swap setting. If you rely on reversed paddles, check this before an activation.

## How POTACAT Keys Your Radio

POTACAT picks a keying route based on your rig and connection. The first key event logs the choice — look for `[CW] Keying route: ...` in the verbose log.

| Route | How it works | Extra hardware |
|---|---|---|
| **CAT text CW** | Sends the message as text over the CAT connection — `KY` on Kenwood/Elecraft/QMX, CI-V `0x17` on Icom. Used by the CW text box and macro buttons. | None |
| **CAT real-time keying** | Keys each dit and dah over CAT — CI-V `0x1C 0x01` (CW key line) on Icom, or `TX1;`/`TX0;` on Yaesu rigs that support it. | None |
| **DTR pin keying** | Toggles the DTR line of a serial port that is wired or routed to the rig's key input. | A rig with a second USB serial port that accepts DTR keying (e.g. QMX, FTDX101, FT-710 CAT-2), or an external USB-serial adapter — see below |

## CW Key Port

The **CW Key Port** setting in **Settings > CW Keyer** selects a *dedicated* serial port whose DTR pin keys the radio. Leave it **(none)** unless you actually have one — for most rigs on a direct serial/CI-V connection, POTACAT keys the radio through the normal CAT link with no extra hardware.

You need a CW Key Port when:

- **Your rig's CAT CW is unreliable.** On the FT-710, for example, the CAT `KY` command raises the carrier but doesn't reliably key Morse — POTACAT keys it via DTR on the CAT-2 serial port instead.
- **Your rig's CAT port can't do real-time keying.** Most Yaesu rigs only accept text (`KY`) over CAT, not per-element paddle keying — an external USB-serial adapter wired to the CW KEY jack fills the gap.
- **You're connected through hamlib/rigctld** (see below).
- **You're on Linux with a USB-CDC rig** (see below).

A cheap FTDI or CH340 USB-serial adapter (~$5) works: wire the adapter's **DTR pin to the tip** and **GND to the sleeve** of a 3.5 mm plug for the rig's key jack.

> **Warning:** The CW Key Port must be a *different* COM port than your CAT connection. Setting both to the same port causes a connect/disconnect loop, and POTACAT will skip the port with a log message telling you so. Also note that common "CI-V data cables" are **not** keying cables — the DTR pin isn't broken out.

## hamlib/rigctld: Macros Only

The hamlib protocol has no per-element CW keying command — it can send CW *text* and toggle PTT, nothing in between. That means over a rigctld connection:

- CW **macros and the text box work** normally.
- **Paddle keying does not.** POTACAT disables the paddle (with a red banner) rather than key a silent carrier. On Icom rigs, hamlib's PTT command raises the mic PTT line while the CW key line stays untouched — the transmitter keys, but no CW goes out.

To use a paddle, either connect the rig via **direct serial / CI-V** instead of rigctld, or add a USB-serial adapter as the **CW Key Port** — DTR keying works regardless of the CAT backend.

## Linux: DTR Keying Limitation

On Linux, the kernel's `cdc_acm` driver (used by USB-CDC rigs like the QMX, QDX, and IC-7300 family connected directly) doesn't support the serial-pin control POTACAT needs for DTR keying. The symptom in the log is `DTR keying not supported on this port` or `setCwKeyDtr error: Operation not supported`.

Your options:

1. **External FTDI/CH340/CP2102 USB-serial adapter** as the CW Key Port — these use a different kernel driver that handles DTR correctly. This is the reliable path.
2. **CW text macros** — they work over the main CAT port without DTR.
3. Windows and macOS are unaffected.

## CW Macros

Five macro buttons send canned CW messages. Both the **label and the text** of each button are editable in **Settings** (search for "CW Macros"), and the buttons also appear in the VFO View and in ECHOCAT.

These variables expand when the macro is sent:

| Variable | Expands to |
|---|---|
| `{call}` | The callsign of the spot you're working |
| `{MYCALL}` | Your callsign |
| `{op_firstname}` | The operator's first name from QRZ lookup (falls back to `OM` if QRZ has no name) |

For example, `{call} DE {MYCALL} GM {op_firstname} TU 73` might go out as `W1AW DE K3ABC GM BOB TU 73`.

> **Note:** Variables must use curly braces — `{call}`, not `[call]` or `(call)`. Anything else is sent as literal text. `{op_firstname}` uses the QRZ first-name field verbatim, which may include a middle initial.

**Stopping a message mid-send:** press **ESC** in the POTACAT CW Macros window, or tap the **HALT/STOP** button next to PTT in ECHOCAT. On rigs with direct text keying (K3, QMX), pressing another macro button interrupts the current message; some users report that Yaesu rigs which play messages from memory finish the queued message first.

> **Tip:** Some operators program macro button 1 as `EE` — a quick way to cut off a longer message you pressed by accident.

## CW from Your Phone

The keyer extends to ECHOCAT: your macro buttons sync from the desktop to the phone automatically (they're stored on the desktop, so you only maintain one set), and speed controls are available in ECHOCAT's CW panel. You can even key a real paddle through your phone from anywhere — see [Remote CW Keying](nested/remote-cw.md).
