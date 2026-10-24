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

## Rig Profiles

> **New in POTACAT 1.13.0** as rig presets; **expanded in 1.13.2** into rig profiles.

A rig profile is a named set of radio settings for the active rig. It can set any of these: **TX power**, **RF gain**, **AF gain** (the radio's speaker level, so 0 silences the shack for FT8), the **RX filter**, **noise blanker**, **noise reduction**, **auto-notch**, **compressor**, **VOX**, **preamp**, **attenuator** and **AGC**. Tick only what the profile should set; everything else on the radio is left as it is.

### Make a profile

1. Open **Settings > Profiles**, or click **Rig** in the top bar and open the **Presets** tab.
2. Click **+ New preset** and give it a name, such as `FT8`.
3. Tick the settings it should include and enter their values, or set the radio the way you want it and click **Use current** to fill every field from the radio.
4. Click **Save**.

Profiles are saved per radio, so each rig in [My Rigs](nested/my-rigs.md) keeps its own set. Settings your radio can't change over CAT show as **Not available on this radio**.

### Apply a profile

Tap a profile in **Settings > Profiles** or the Rig menu's **Presets** tab. Profiles are also listed in the VFO window and in ECHOCAT (the app and ECHOCAT Web). A [second POTACAT driving your shack](nested/remote-desktop.md) can apply them too.

### Let the mode and band apply it

- **By mode:** under **Apply by itself when the mode changes to**, assign one profile to each mode family: **SSB**, **CW**, **Digital**, **FM** or **AM**. All SSB can use one profile and all digital another. Starting FT8 applies the Digital one.
- **By band:** for finer control, add **Band rules** with **+ Add rule**, such as "20 m SSB uses this, 40 m SSB uses that". A rule can name a band, a mode, or both; no band picked means any band. Rules are checked first, top to bottom, and the first match wins. The mode list is the fallback.

The shack applies a profile the moment the radio moves into a matching mode or band, whatever caused the change: a spot click, the radio's knob, the phone, or an FT8 session starting. A profile goes on before the first transmission and is never applied while the radio is keyed.

> **Example:** hunting POTA on SSB at 100 W, then switching to FT8 at 60 W with the speaker off. Make an `SSB` profile (TX power 100) and an `FT8` profile (TX power 60, AF gain 0), assign them to SSB and Digital, and the radio follows the mode.
