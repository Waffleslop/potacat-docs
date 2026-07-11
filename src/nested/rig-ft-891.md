# Yaesu FT-891

**Best for:** Yaesu FT-891, typically paired with a Digirig (DR-891) interface for CAT and audio.

The settings below are the community reference setup for the FT-891 with a Digirig DR-891. For connection-method background, see [Radio Setup](../radio-setup.md).

## Connection settings

1. Add a new rig → select **Serial CAT (Kenwood)** ([details](serial-cat-kenwood.md))
2. Choose the CP210x COM port
3. Set the baud rate to `38400` (matching **05-06 CAT RATE**)
4. Click **Test Connection**, then Save

> **Tip:** If the test fails, toggle **Disable DTR/RTS on connect** — adapters differ, and this checkbox resolves connection failures in both directions.

- **Linux:** prefer Serial CAT over the Hamlib path with this radio. Add yourself to the serial group (`sudo usermod -aG dialout $USER`, then log out fully) and make sure no other app (FLRig, a logger) is holding the port.
- **macOS:** pick the `/dev/cu.*` serial device. Serial CAT direct to the port works; if you want Hamlib, bridge through FLRig at `127.0.0.1:12345` instead of pointing Hamlib at the serial port.

## Radio menu settings

| Menu | Name | Set to |
|------|------|--------|
| **05-06** | CAT RATE | `38400` |
| **05-07** | CAT TOT | `3000` |
| **05-08** | CAT RTS | `DISABLE` |
| **07-12** | PC KEYING | `OFF` |
| **08-01** | DATA MODE | `OTHERS` |
| **08-05** | DATA LCUT FREQ | `OFF` |
| **08-07** | DATA HCUT FREQ | `OFF` |
| **08-09** | DATA IN SELECT | `REAR` |
| **08-10** | DATA PTT SELECT | `DAKY` |
| **08-11** | DATA OUT LEVEL | `50` |
| **08-12** | DATA BFO | `USB` |
| **16-03** | HF PWR | `40` W |
| **16-14** | DATA GAIN | `50` |

## CW keying

> **Warning:** The FT-891's `KY` CAT command has no free-text form, so **CW text macros key the transmitter but produce zero RF** on this radio (same limitation as the FT-991A). This is a known open limitation.

For working remote CW, key the radio's DTR line instead of CAT:

- Wire a cheap FTDI/CH340 USB-serial adapter to the radio's **KEY** jack and select it as the **CW Key Port** in POTACAT Settings.
- Make sure break-in (**BK-IN**) is enabled on the radio, or it will sidetone without transmitting.

## Audio & digital modes

- The DATA menu settings above (08-01 through 08-12) route digital-mode TX audio through the rear port — required for JTCAT/FT8 through the Digirig.
- **11-06 SSB OUT LEVEL** directly sets how loud ECHOCAT's RX audio is.
- **11-05 SSB MIC SELECT** picks the SSB TX audio source: if it's set to `MIC`, the hand mic — not your remote audio — is what transmits when ECHOCAT keys the radio.

## Known quirks

CAT-level facts about this radio (useful with **Rig → Custom Command**):

- RF gain over CAT spans `000`–`030`, not 0–255 as the CAT manual states — POTACAT's rig profile accounts for this.
- TX power range is 5–100 W; the rig clamps at 5 W minimum.
- ATU: send `AC002;` alone to start a tune cycle (`AC001; AC002;` together fails); `AC000;` turns the tuner off.
- Filter width is `SH01xx;` — `SH0xx;` is IF shift, a different control.
- Split is `ST1;`, not `FT1;`.
