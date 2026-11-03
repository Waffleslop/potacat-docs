# SSTV

POTACAT receives and sends slow-scan TV pictures with nothing else to install. Open **More ▾ > SSTV**.

- **Receive:** pick a calling frequency with the frequency button at the top left, or type another frequency in kHz and press Enter. Pictures appear as they arrive and are saved to the **Received** tab. A picture from a weak signal is shown but not saved automatically; press **Keep** to save it. **Fix slant** and **Redecode** straighten a slanted picture.
- **Send:** build a picture in the compose area (**Photo…** for a background, **+ Text** for text, or a template from the **Templates** tab), then press **TRANSMIT**. Double-click a received picture, or press **↩ Reply**, to answer it.
- **How SSTV contacts work**, under the ⚙ gear, explains the usual exchange.

SSTV also works from ECHOCAT and from [another POTACAT](remote-desktop.md#sstv).

## Audio and Drive

- SSTV uses the radio's audio devices from **Settings > My Rigs**, the same ones as JTCAT. To use different devices for SSTV only, choose them under ⚙ > **Audio** > **Receive** and **Transmit**. If SSTV misbehaves and JTCAT doesn't, check these first: an old device chosen here overrides the radio's.
- **Drive**, in the SSTV window's top bar, is the audio level SSTV sends to the radio. It is **separate from JTCAT's Drive** and starts at 50%. The **PWR** and **SWR** meters beside it show the radio's output live while transmitting.

## No power out on SSTV, but FT8 works

The radio keys, but little or nothing goes out, while JTCAT FT8 reaches full power on the same radio. Check in this order:

1. **Drive** in the SSTV window. It is its own slider; raise it while watching **PWR**.
2. **⚙ > Audio > Transmit** in the SSTV window. It should be blank (follow My Rigs) or the radio's sound card, not the computer's speakers or an old device.
3. **The radio's mode while SSTV transmits.** JTCAT puts the radio in its data mode (DATA-U, USB-D, DIGU, DATA A), where it takes audio from USB. SSTV may transmit in plain USB or LSB, and many radios take USB/LSB audio from the front microphone, so the computer's audio never reaches the transmitter. Watch the radio's mode display while you transmit. If it shows USB or LSB:
   - set the radio's modulation source for SSB (voice) to its USB or rear input in the radio's menu, or
   - put the radio in its data mode before pressing **TRANSMIT**.
4. **Levels outside POTACAT:** the radio's USB or data MOD level, and on Linux the sound card's output level in the system sound settings.

Watch the ALC as you raise Drive, as for FT8; see [Transmit Level: TX Pwr, Drive and ALC](jtcat.md#transmit-level-tx-pwr-drive-and-alc).
