# WSJT-X

POTACAT listens for WSJT-X UDP messages (default port 2237) and cross-references decoded callsigns against active POTA spots.

> **Note:** You don't need WSJT-X to work FT8 in POTACAT — [JTCAT](jtcat.md) is POTACAT's built-in FT8/FT4 engine. This page is for operators who prefer to run the separate WSJT-X application and have POTACAT work alongside it. If you're using JTCAT, leave the **WSJT-X** mode checkbox unchecked.

**Features:**
- POTA activators in the WSJT-X decode list are highlighted green
- Decode indicators appear on matching rows in the POTACAT spot table
- Click-to-tune sends the frequency to your FlexRadio via SmartSDR TCP (no CAT conflict with WSJT-X)
- Auto-log: QSOs completed in WSJT-X can be automatically logged in POTACAT and forwarded to your external logbooks

Enable WSJT-X in **Settings → Spot Sources**. Set the UDP port to match your WSJT-X configuration.

## Who Controls the Radio?

Two applications can't both run CAT control of the same radio. If WSJT-X and POTACAT need the same rig, you have two options.

### Option A — WSJT-X Mode (simplest)

Check the **WSJT-X** mode checkbox under the **CAT** pill. In this mode:

- **POTACAT's own CAT control is disabled.** Instead of talking to the radio directly, POTACAT sends UDP packets to WSJT-X, and WSJT-X controls the rig through its own CAT connection.
- Clicking a spot in POTACAT asks WSJT-X to QSY the radio.
- Because POTACAT isn't holding the serial port, there is no COM-port conflict.

> **Warning:** While WSJT-X Mode is enabled, POTACAT features that need direct rig control — including [JTCAT](jtcat.md) — are unavailable. Uncheck it when you return to normal operation. If clicking a spot suddenly "does nothing," a leftover WSJT-X Mode checkbox is a prime suspect.

FlexRadio owners get a bonus: click-to-tune goes through the SmartSDR TCP API, which works even while WSJT-X owns CAT.

### Option B — Share the rig through rigctld

Run a networked `rigctld` yourself and point both applications at it:

1. Start rigctld (Hamlib) for your radio, e.g. on `127.0.0.1:4532`.
2. In POTACAT, choose the **rigctld Network** connection type with that host and port.
3. In WSJT-X, set the rig to **Hamlib NET rigctl** with the same address.

Both apps keep full rig control, and CAT survives either application closing.

> **Warning:** Don't use POTACAT's **Other (Hamlib)** connection type for this — it spawns its own internal rigctld, which would conflict with yours and shuts down when POTACAT exits, orphaning WSJT-X. Run a standalone rigctld instead.

## UDP Port 2237 Basics

- `2237` is the conventional WSJT-X UDP server port. Set it in WSJT-X under **File → Settings → Reporting**, and make POTACAT's port match.
- POTACAT opens the port with **port sharing enabled**, so other listeners (GridTracker, ACLog, and friends) can share 2237 — WSJT-X broadcasts to all listeners on the port.
- If another application refuses to share the port, move POTACAT to a different port and use a JTAlert-style UDP relay to feed both.

## Launch Order for Logger Chains

If you chain WSJT-X → POTACAT → an external logger (N3FJP, ACLog, and similar), start the programs in that order:

1. **WSJT-X** — controls the radio and produces the UDP stream.
2. **POTACAT** — attaches to the UDP stream.
3. **Your logger** — receives forwarded QSOs from POTACAT.

When you click **OK** on the WSJT-X log window, POTACAT auto-logs the QSO, matches the callsign against spotted POTA activators so the park is marked worked, and forwards the QSO to your configured logbooks — see [Logbook Forwarding](logbook-forwarding.md).

> **Tip:** Starting a logger before POTACAT can leave it holding a port POTACAT needs. If forwarding or rig control fails right after startup, close everything and relaunch in the order above.

## FT4 and FT2 in ADIF Exports

POTACAT exports FT4 and FT2 QSOs as `MODE=MFSK` with `SUBMODE=FT4` (or `SUBMODE=FT2`), as the ADIF specification requires — files with a plain `MODE=FT4` are rejected by the POTA uploader. Keep this in mind if you hand-edit exported logs.
