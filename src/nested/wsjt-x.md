# WSJT-X

POTACAT listens for WSJT-X UDP messages (default port 2237) and cross-references decoded callsigns against active POTA spots.

> **Note:** You don't need WSJT-X to work FT8 in POTACAT — [JTCAT](jtcat.md) is POTACAT's built-in FT8/FT4 engine. This page is for operators who prefer to run the separate WSJT-X application and have POTACAT work alongside it. If you're using JTCAT, leave **WSJT-X Mode** off.

**Features:**
- POTA activators in the WSJT-X decode list are highlighted green
- Decode indicators appear on matching rows in the POTACAT spot table
- Click-to-tune sends the frequency to your FlexRadio via SmartSDR TCP (no CAT conflict with WSJT-X)
- Auto-log: QSOs completed in WSJT-X can be automatically logged in POTACAT and forwarded to your external logbooks

Turn on **WSJT-X Mode** in **Settings > Spots**, and set **UDP Port** to match WSJT-X. The same section has **Highlight POTA activators in WSJT-X** and **Auto-log WSJT-X QSOs to POTACAT**. Before 1.14.5 this box was called **WSJT-X Integration**; it is the same setting. The same check box is in the CAT menu: click **CAT** in the top bar.

> **Warning:** With **WSJT-X Mode** on, POTACAT leaves the radio to WSJT-X and gives up its own CAT control. It asks before turning on. There is no way to listen to WSJT-X's UDP messages and keep POTACAT's own CAT.

### How to tell it is on, and how to turn it off

> **New in POTACAT 1.14.5.**

- An amber **WSJT-X Mode** chip leads the top bar, and **CAT** shows **off**. (Before 1.14.5 the CAT light could still show green.)
- Click either one for a panel at the top of the CAT menu: what the mode does, whether WSJT-X is heard, and a one-click **Turn off WSJT-X Mode**. You can also click **CAT** in the top bar and untick **WSJT-X Mode**.
- If the mode is on and WSJT-X isn't heard 30 seconds after start, POTACAT says so.
- Station Setup and Report a Bug say when it is on, and ECHOCAT Web shows the same chip.

## Who Controls the Radio?

Two applications can't both run CAT control of the same radio. If WSJT-X and POTACAT need the same rig, you have three options.

### Option A — WSJT-X Mode (simplest)

Turn on **WSJT-X Mode**, in **Settings > Spots** or in the CAT menu (click **CAT** in the top bar). In this mode:

- **POTACAT's own CAT control is disabled.** POTACAT disconnects from the radio, and WSJT-X controls the rig through its own CAT connection. POTACAT listens to WSJT-X's UDP messages for highlights, decodes and auto-log.
- Clicking a spot in POTACAT doesn't move the radio, and nothing is sent to WSJT-X. The exception is a FlexRadio (see below).
- Because POTACAT isn't holding the serial port, there is no COM-port conflict.

> **Warning:** While WSJT-X Mode is enabled, POTACAT features that need direct rig control — including [JTCAT](jtcat.md) — are unavailable. Turn it off when you return to normal operation. If clicking a spot suddenly "does nothing," look for the amber **WSJT-X Mode** chip in the top bar.

FlexRadio owners get a bonus: click-to-tune goes through the SmartSDR TCP API, which works even while WSJT-X owns CAT.

### Option B — Share the rig through rigctld

Run a networked `rigctld` yourself and point both applications at it:

1. Start rigctld (Hamlib) for your radio, e.g. on `127.0.0.1:4532`.
2. In POTACAT, choose the **rigctld Network** connection type with that host and port.
3. In WSJT-X, set the rig to **Hamlib NET rigctl** with the same address.

Both apps keep full rig control, and CAT survives either application closing.

Option B can't be combined with **WSJT-X Mode**. Turning that on disconnects POTACAT's CAT, so Option B ends. With Option B you get shared rig control, but no WSJT-X highlights, decodes or auto-log in POTACAT.

> **Warning:** Don't use POTACAT's **Other (Hamlib)** connection type for this — it spawns its own internal rigctld, which would conflict with yours and shuts down when POTACAT exits, orphaning WSJT-X. Run a standalone rigctld instead.

### Option C — Share the rig through flrig

POTACAT has a connection type **FLRig (a shared radio)**: flrig holds the radio and POTACAT is one of its clients, beside your logger or fldigi. WSJT-X can be another client of the same flrig. How to point WSJT-X at flrig is in WSJT-X's own manual; it hasn't been checked for this guide.

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

As of 1.14.3, POTACAT writes FT4 contacts as `MODE=FT4` and FT2 contacts as `MODE=FT2`, with no `SUBMODE`.
