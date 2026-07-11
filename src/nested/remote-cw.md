# Remote CW Keying

ECHOCAT lets you send real CW — your own fist, on your own paddle — through the radio in your shack from anywhere your phone can reach it. This page covers the remote keying chain; for the desktop keyer itself (keyer modes, WinKeyer, CW Key Port, macros), see the [CW Keyer](../cw-keyer.md) page.

## How It Works

```
paddle/adapter → phone browser (keyboard or MIDI events) → WebSocket → desktop POTACAT → IambicKeyer → radio
```

Your paddle adapter sends keyboard or MIDI events to the ECHOCAT page on your phone. ECHOCAT forwards dit/dah events over the WebSocket to desktop POTACAT, whose IambicKeyer state machine generates the element timing and keys the radio — via a CAT command or a DTR pin, depending on your rig. The sidetone is generated locally on the phone, so it fires the instant you press the paddle.

You don't need a paddle at all to work CW remotely: the CW text box and the five macro buttons send CW via CAT on supported rigs.

## Enabling It

1. On the desktop, open **Settings > ECHOCAT** and check **Enable Remote CW Keyer**. This is the one that matters for phone keying — you do *not* need the desktop **Enable CW Keyer** checkbox (that's for local keying on the PC).
2. Leave **CW Key Port** set to **(none)** unless you have an external USB-serial adapter plugged into your radio's key jack (see [when you need one](../cw-keyer.md#cw-key-port)). On rigs like the IC-7300, POTACAT keys the radio directly through the CI-V connection with no extra hardware.
3. On your phone, the CW panel appears at the bottom when you're tuned to a CW frequency. If it says **CW unavailable**, the Remote CW Keyer setting isn't enabled on the desktop.

> **Tip:** The first key event writes `[CW] Keying route: ...` to the verbose CAT log. If you see no `[CW]` lines at all, your paddle events aren't reaching the desktop — check the phone-to-desktop connection before suspecting the radio.

## Supported Key Hardware

| Hardware | Sends | Notes |
|---|---|---|
| **N6ARA TinyMIDI** | Keyboard mode: `[` (dit) and `]` (dah); MIDI mode also works | Keyboard mode is the reliable path on iPhone |
| **Vail adapter** | Left Ctrl (dit) / Right Ctrl (dah) | Keyboard emulator |
| **VBand dongle** | Left Ctrl (dit) / Right Ctrl (dah) | Same scheme as Vail |
| **K1EL WinKeyer** | Connects to the *desktop*, not the phone | Configure under **Settings > CW Keyer** on the PC |
| Anything that types characters (e.g. Morserino as a Bluetooth keyboard) | Text | Fills the CW text box — not paddle keying |

### Keyboard mode vs. MIDI mode

- **iOS Safari does not support Web MIDI** — use keyboard mode on iPhone/iPad.
- **Android MIDI** needs a Chromium-based browser *plus* a BLE-MIDI bridge app from the Play Store to link the adapter.
- Keyboard mode has one downside: the adapter becomes a keyboard, so your phone's pop-up keyboard disappears while it's connected.
- The native ECHOCAT iOS/Android apps support MIDI natively — no browser workarounds needed.

## On-Screen Straight Key

No hardware handy? The ECHOCAT app has an on-screen straight key: enable it under **Settings > C.W. Keyer** in ECHOCAT, and a **Key** button appears in place of PTT on CW frequencies. Hold it down to key — it's your fist, rough edges and all, rather than a stored message.

## Latency Expectations

- **Sidetone is instant.** It's generated on the phone, so there's no perceptible delay between paddle press and sidetone, regardless of network conditions.
- **The RF side follows your network.** Local sidetone doesn't change when the radio actually keys — the transmitted elements are timed by the desktop keyer, but they start after the round trip to your shack.
- Use **wired headphones** — Bluetooth adds noticeable audio lag.
- Mobile browsers take a moment to warm up audio at the start of a session; a one-time "click" when audio unlocks is the phone's audio hardware waking up and is normal.
- Any VPN that lets your phone reach the shack PC works — Tailscale is popular but not required.

## Rig Recipes

### QRP Labs QMX

> **Note:** QMX firmware **1.03 or later** is required for DTR keying on the second USB port.

A known-good setup:

1. POTACAT rig: **Serial CAT (Kenwood)** on the QMX's first USB port at `38400` baud, with **Disable DTR/RTS on connect** checked
2. Audio in/out: the QMX Digital Audio Interface
3. QMX menus: **System/GPS & Ser. Ports > Serial Ports** = `2`, and **CW/CW Keyer > Key from USB DTR** = `USB 2`
4. **CW Key Port (DTR Keying)**: the QMX's *second* COM port

### Icom IC-7300 / IC-705 / IC-7610

Set the rig menu **MENU > SET > Connectors > USB Keying (CW)** = `USB(A) DTR` (preferred), or **USB SEND** = `DTR`. POTACAT prints this menu path in the log when it routes keying via the main port's DTR line.

> **Warning:** Remote CW on Icom requires a **direct CI-V serial connection**, not rigctld/hamlib. On direct CI-V, POTACAT sends a CI-V "CW key down/up" command for each paddle element. Hamlib has no such command — it only exposes the mic PTT line — so paddle keying over rigctld puts the transmitter on with the CW key line untouched: a silent key-down.

### Yaesu

Most Yaesu CAT ports only accept text CW (the `KY` command), not real-time paddle keying. To key a paddle on a Yaesu, set **CW Key Port** to a USB-serial adapter wired to the radio's key jack. Exceptions and specifics:

- **FTDX101D**: real-time keying works over CAT (`TX1;`/`TX0;`) — no DTR adapter needed.
- **FT-710**: even *text* CW over `KY` is unreliable on this rig. Set **CW Key Port** to the radio's **CAT-2** serial port (the second COM port, e.g. `COM<n+1>`), and on the radio set **OPERATION SETTING > CAT/LINEAR/TUNER > USB Keying (CW)** = `DTR`. Also set **CAT-1 TIME OUT TIMER** = `1000 ms` and turn **CW BK-IN** on.

## Known Limitations

- **Yaesu FT-891 / FT-991A: text CW keys the transmitter but produces zero RF.** The 991A's `KY` command has no free-text form — the text is silently ignored while the TX light comes on — and the FT-891 shows the same symptom. This is a known open limitation of text/macro CW on these rigs.
- **Break-in must be on.** If the radio keys and you hear sidetone but no RF goes out, check that break-in (**BK-IN**) is enabled — and note the FTDX10 remembers the break-in setting *per band*.
- **Linux DTR limitation.** The `cdc_acm` kernel driver used by USB-CDC rigs (QMX, QDX, IC-7300 family) can't control the DTR pin, so paddle keying fails with `Operation not supported`. The fix is a ~$5 FTDI or CH340 USB-serial adapter wired to the rig's key jack, set as the **CW Key Port** — its driver handles DTR correctly. CW text macros still work over the main CAT port. Windows and macOS are unaffected. See [the CW Keyer page](../cw-keyer.md#linux-dtr-keying-limitation) for details.
- Some users on Samsung Android phones report truncated sidetone and the radio not keying with TinyMIDI/VBand adapters in the browser; the native mobile apps are the recommended path there.

## Stopping a Transmission

Tap the **HALT/STOP** button next to PTT in ECHOCAT (or press **ESC** in the desktop CW Macros window) to stop a macro mid-send.
