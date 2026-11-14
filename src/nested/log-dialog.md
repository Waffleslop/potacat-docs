# Log Dialog

> **Note:** Logging is always on. There is no setting to enable it.

Click the **Log** button on any spot row, map popup, or use **Ctrl+L** for an unspotted QSO. The dialog pre-fills:

- Callsign, frequency, mode, band (from the spot)
- Operator name (from QRZ lookup)
- RST Sent and Received (split-digit boxes with auto-advance)
- TX Power. From 1.14.5 this is the power the radio reports or the power POTACAT set, else the **Default TX Power (W)** you typed in **Settings > Logging**, else nothing. That box is empty until you fill it. Before 1.14.5, a contact was logged at 100 W when POTACAT could not read the radio's power
- Park/summit reference
- "Spot on DX Cluster" checkbox (for non-park contacts)

Press **Enter** to save.

**Ctrl+L** with a spot tuned opens the dialog as POTA (or SOTA, WWFF) with the reference filled in, just like the **Log** button. Change the callsign and POTACAT looks up that operator instead, so the second op at a multi-op activation gets their own name from QRZ.

**Move it out of the way:** drag the dialog by its title bar so it doesn't cover the callsigns you are logging. It opens where you left it next time. Double-click the title bar to centre it again.

## Multiple Operators and Parks

- **Pass-the-mic activations:** enter every operator's callsign comma-separated in the callsign field (e.g. `K1ABC, W2DEF`) — POTACAT logs a separate entry for each operator.
- **n-fer hunts:** enter the park references comma-separated in the reference field to credit every park the activator is sitting in.

## Auto-Respot

Logging a POTA QSO automatically re-spots the activator (you can turn this off). The respot option, with an editable comment, lives at the bottom of the dialog.


