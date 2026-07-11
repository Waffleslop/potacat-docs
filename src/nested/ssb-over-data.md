# SSB over Data

If your radio suddenly flips to `USB-D`, `DATA-U`, `PKTUSB`, or `DIGU` the moment you key PTT from your phone — and your shack microphone goes dead — you've met **SSB over Data**. It looks alarming, but it's a feature working as designed, and it's the most frequently reported "bug" that isn't one.

## What it does

When you press PTT from [ECHOCAT](../echocat.md), POTACAT switches the radio from SSB into its DATA mode for the duration of the transmission, then restores the original mode when you release. In DATA mode the radio takes TX audio from its **USB codec (rear input)** instead of the front mic jack — so your voice from the phone goes out over the air, and the shack mic is effectively muted. The verbose log shows it happening:

```
[PTT] USB -> DIGU (SSB-over-DATA: mic disabled)
```

The setting applies to non-Flex radios and only kicks in when audio is actually streaming through the USB codec — an ECHOCAT session, voice macros, or FreeDV.

## Why it exists

It solves the remote-operation audio path. In plain SSB mode, many radios take TX audio only from the mic jack, and on many rigs the shack mic **stays live** during a remote transmission — anything happening in the shack would be transmitted along with your voice. Flipping to DATA mode routes audio through the USB codec and silences the local mic in one move.

## "But I'm sitting right at the radio!"

If you operate mic-in-hand, you don't want this behavior — DATA mode disables the very mic you're speaking into, so TX comes out silent. To turn it off:

1. Open **Settings** and search for `SSB over Data`
2. Uncheck it and save

> **Tip:** On Yaesu rigs there's an alternative that keeps remote audio working *without* mode flips: leave SSB over Data off and set the radio's **SSB MOD SOURCE** to `REAR` and **REAR SELECT** to `USB`. Remote audio then flows through the rear USB input in regular SSB mode, and the hand mic still works normally — pressing the mic's own PTT re-selects the mic as the audio source.

## Yaesu companion settings

If you keep SSB over Data enabled on a Yaesu, set these radio menus or your transmissions can land off frequency:

| Radio menu | Set to | Why |
|------------|--------|-----|
| **DATA MODE** | `Others` | With the default `PSK` setting, the radio shifts TX about 1.5 kHz below the dial in DATA mode. On the FTDX10 this same change fixes the ±600 Hz DATA-mode TX offset. |
| **SSB MOD SOURCE** | `REAR` | SSB TX audio comes from the rear port instead of the mic jack. |
| **REAR SELECT** | `USB` | The rear port sources audio from the USB codec — where POTACAT sends it. |
| **RPORT GAIN** (FTDX101D) | Start around `1` | The default of 50 is far too hot and distorts badly. Increase slowly while watching ALC. |

## Rig-specific notes

- **FT-710** — works well with SSB over Data. The radio showing `DATA-U` in red while you key from the phone is normal and expected.
- **Kenwood TS-890 and similar** — the USB → USB-D flip on PTT is this feature, not a malfunction.
- **FTDX10 / FTDX3000** — the DATA-mode filter on these rigs is limited to about 2.4 kHz, and SSB over Data is known to misbehave on them (mode stuck in DATA, off-frequency TX, a vanishing PTT button). **Disable SSB over Data** on these radios. On the FTDX3000, also set menu **103** to `USB` so rear-port audio still comes from the USB codec.
- **IC-7300** — some users report that intermittent PTT through the app clears up with SSB over Data turned off.
