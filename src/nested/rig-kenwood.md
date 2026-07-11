# Kenwood TS-590, TS-890S, TS-2000 & TS-480

Kenwood rigs connect over **Serial CAT (Kenwood)** — the basic hookup (COM port, baud, Test Connection) is covered in [Serial CAT (Kenwood)](serial-cat-kenwood.md). This page covers the model-specific quirks.

## TS-590S / TS-590SG

### Connection

- Use the radio's **USB-B** port, not the ACC or COM connectors.
- The default baud rate is `9600`. To change it, use radio menu **68** — and note you must **power-cycle the radio** for a baud change to take effect.
- If you get "no response from radio": match the baud on both sides, toggle **Disable DTR/RTS on connect** (USB adapters differ), and close every other program that could be holding the COM port.

### Rear (USB) audio: `TX;` vs `TX1;`

The 590 family selects its TX audio source with the keying command itself:

| Command | Keys the radio with |
|---|---|
| `TX;` | Front **mic** input |
| `TX1;` | **Rear/USB** audio input |

POTACAT keys the rear input for digital modes and remote audio. If your radio keys up but transmits silence on FT8, SSTV, or ECHOCAT voice, you're seeing the front-mic behavior — send `TX1;` as a custom CAT command to confirm: with `TX1;` the radio transmits the USB audio correctly.

> **Note:** The radio may still beep on each keying command — that's normal.

### ECHOCAT

With the radio in DATA mode, the PTT button disappears from ECHOCAT — that's by design (PTT is shown for SSB/FreeDV only). Take the radio out of data mode to get it back.

## TS-890S

When you PTT from your phone, the radio flips **USB → USB-D**. That's the **SSB-over-DATA** feature working as designed: it routes your phone's voice through the radio's USB audio input, mutes the shack mic, and restores the mode when you release PTT.

If you operate with the radio's own mic in hand, uncheck **SSB-over-DATA** in Settings (search for "SSB over Data") — otherwise the mode switch disables the very mic you're speaking into.

## TS-2000

- **No SWR over CAT**: the TS-2000 doesn't expose an SWR reading via CAT, so POTACAT's SWR bar stays dashed out. That's normal, not a fault.
- **Set the Radio Model to `TS-2000`**: with a generic or empty model selected, POTACAT polls commands the radio doesn't support, each one triggers the radio's `?;` error response — and the radio **beeps continuously**. Older Kenwoods (e.g. TS-850S) beep for the same reason; always pick the closest model.
- **Radio jumping into split when tuning?** Check POTACAT's **Enable Split Mode** setting first — when it's on, POTACAT deliberately sets up split on every QSY. This applies to all Kenwood-protocol rigs.

## TS-480

If the S-meter and power readings look far too low and SWR shows blank in ECHOCAT, update POTACAT — early builds converted TS-480 meter values with FlexRadio scaling by mistake.

## Other radios that speak Kenwood

The **FX4CR** (F5BUD firmware) presents itself to CAT software as a TS-590S — set it up exactly like a TS-590S over Serial CAT (Kenwood).
