# Radio Setup

POTACAT supports five connection methods. Open Settings and click **Add Rig** to configure your radio.

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
