# Radio Setup

POTACAT supports five connection methods. Open Settings and click **Add Rig** to configure your radio.

## Let N1MM+ (or Another Logger) Control the Radio

> **New in POTACAT 1.13.1.**

POTACAT can pretend to be a Kenwood TS-2000 on this PC and pass everything N1MM+ sends on to the radio it controls, so you don't have to fight over the CAT port.

1. In POTACAT, turn on **Settings > Tuning > Let N1MM+ (or another logger) control the radio**. Note the **Port** (4535 by default).
2. In N1MM+, open **Config > Configure Ports** and set **Port** to **TCP**, **Radio** to **TS-2000**, the address to `127.0.0.1` and the port to the one from step 1.

Frequency, band changes, mode, PTT and CW (sent as CAT text) all go through POTACAT. That includes a [remote shack you are driving](nested/remote-desktop.md) from this PC, so N1MM+ on a laptop works the shack's radio.

> **Note:** N1MM's own voice keyer plays through this PC's sound card, not the shack's. For remote SSB, use POTACAT's voice macros instead.

Other loggers that can talk to a TS-2000 over TCP can use the same setting.

## Sound-Card PTT for Radios with No CAT

> **New in POTACAT 1.13.1.**

A radio with no computer control, such as a Baofeng on a Digirig Lite or a CM108/CM119 cable, can still be keyed from POTACAT:

1. Add the radio with **No CAT control (VOX)** as its connection type.
2. Under **Transmit (PTT)**, choose **The USB sound card keys it (Digirig Lite, CM108 / CM119 PTT)**.
3. Leave **PTT pin** on **GPIO 3** (right for the Digirig Lite and most cables) unless your interface says otherwise, then click **Find the sound card**.

PTT then keys from any surface: this PC, ECHOCAT on your phone, or FT8.

> **Linux:** your user needs read/write access to the sound card's `hidraw` device. Add the udev rule Dire Wolf documents for CM108 PTT.

## Rig Presets

> **New in POTACAT 1.13.0.**

A rig preset is a named set of **TX power**, **RF gain** and **AF gain** — AF gain is the radio's speaker level, so 0 silences the shack, which is handy for FT8. Apply one with a single tap instead of setting three levels by hand.

### Make a preset

1. Click **Rig** in the top bar and open the **Presets** tab.
2. Click **+ New preset** and give it a name, such as `FT8`.
3. Enter the levels, or click **Use current** to fill them from the radio's present settings. A blank field leaves that level alone.
4. Click **Save**.

Presets are saved per radio, so each rig in [My Rigs](nested/my-rigs.md) keeps its own set.

### Apply a preset

Tap a preset in the **Presets** tab. They are also listed in the VFO window, in ECHOCAT Web, and — when the app update lands — in the ECHOCAT app. A [second POTACAT driving your shack](nested/remote-desktop.md) can apply them too.

### Let the mode apply it

Under **Apply by itself when the mode changes to**, assign a preset to **SSB**, **CW**, **Digital**, **FM** or **AM**. The shack applies it the moment the radio moves into that mode family, whatever caused the change: a spot click, the radio's knob, the phone, or an FT8 session starting.

A preset goes on before the first transmission and is never applied while the radio is keyed.

> **Example:** hunting POTA on SSB at 100 W, then switching to FT8 at 60 W with the speaker off. Make an `SSB` preset (TX power 100) and an `FT8` preset (TX power 60, AF gain 0), assign them to SSB and Digital, and the radio follows the mode.

Fields your radio can't set over CAT are hidden, with a note saying why.
