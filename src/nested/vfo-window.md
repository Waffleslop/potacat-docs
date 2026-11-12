# VFO Window

The VFO window is a separate window for running the radio: the frequency dial, mode and band, meters, the radio's own controls, your profiles, the speaker and PTT. Open it with the **VFO** button in the main window. It reopens at the size, place and width you left it.

## Two sizes: Large VFO and Small VFO

> **New in POTACAT 1.14.3.**

The button beside the gear in the window's title bar switches between the two sizes.

- **Large VFO** is the full window.
- **Small VFO** is one line. By default it shows the frequency, mode, band, S-meter, **Scan**, **Audio**, **Volume**, **PTT** and **Log**.

The Small VFO always stays on one line. In a narrow window, the items at the end of its list hide first. The frequency and PTT always stay.

On the Small VFO:

- **Scan** starts and stops the main window's spot scan. It reads **Stop** while a scan is running, even one started from your phone.
- The gear opens the Large VFO with its settings. **Done** takes you back to the Small VFO.

## Choose what each size shows

Click the gear to open VFO settings. There is a **Large VFO** tab and a **Small VFO** tab. Each one is a single list:

- Tick a row to show it.
- Move a row with the arrows, or drag it.

The Small VFO tab shows a preview of the line as you change it. **Reset Large VFO to default** and **Reset Small VFO to default** put a list back as it came.

Before 1.14.3, VFO settings had two separate lists, **Show in this window** and **Order**. They are now this one list per size. If you had already arranged your window, your order is kept.

### CAT buttons

Under **CAT buttons** in VFO settings, choose which of the radio's controls to show: NB, NR, ANF, APF, Preamp, Att, COMP, VOX, MON, RIT, Split and ATU. Only the ones your radio supports are offered. The Small VFO can show your custom CAT buttons too.

## What's in the window

- **Frequency.** Turn the knob, scroll the mouse wheel (up tunes up, from 1.14.2), or type a frequency. On 2 m, 1.25 m, 70 cm and 23 cm a bare number is read as kHz, so `432100` tunes 432.100 MHz. The VFO window and the Band Scope share one tuning step.
- **Power.** A **Power** row sits under the filter slider (from 1.14.2). It follows the main window's power control and uses the same limits, including **Full power (W)** and a Guest Pass cap.
- **Profiles and presets.** Your rig profiles sit in a drop-down under the dial. See [Radio Setup](../radio-setup.md).
- **Audio.** The speaker button reads **Audio on** or **Audio off**, so it says in words whether you can hear the radio. The volume knob also sets the SDR's audio when you listen through one.
- **PTT.** From 1.14.2, the window shows a notice when the microphone it opened is the radio's own receive audio, is blocked, or is silent. Every PTT press logs the microphone, the output and the level.
- **WebSDR.** In a new Large VFO the WebSDR block sits under the knob. See [WebSDR, KiwiSDR and RTL-SDR Receive](websdr.md).
- **Favorites.** The Landmarks and Channels you starred in [Directory](directory.md#favorites).
- **Radio.** At the bottom, **Power On** and **Power Off** for a radio that can be switched over CAT. **Power Off** asks for a second press.

The same window drives the radio at home when this POTACAT is [paired with a remote shack](remote-desktop.md).
