# DXLab Commander

> **New in POTACAT 1.13.10.**

If you run DXLab Suite, POTACAT can control your radio through **DXLab Commander** instead of opening the radio's port itself. Commander keeps the radio, and DXKeeper, Spot Collector and POTACAT all follow it.

## What works

Through Commander, POTACAT handles **frequency, mode, split, PTT and CW text**. For controls Commander has no TCP command for, such as noise blanker, noise reduction or the ATU, you can have POTACAT run one of Commander's command sequences (see [below](#command-sequences)).

## Set it up

1. Start **Commander**. It must be running whenever POTACAT is.
2. In Commander's **Net Serv** window, note the **Base Port** (52000 by default).
3. In POTACAT, open **Settings > My Rigs**, add or edit the rig, and choose **DXLab Commander**.
4. Set **Radio Model** to your radio, so POTACAT knows its bands and power limits.
5. **Host:** `127.0.0.1` if Commander runs on this PC.
6. **Port:** Commander's Base Port **plus 2**. With the default Base Port, that's `52002`.
7. **Decimal point:** match the Windows number format on the computer running Commander, **Period (1,234.5)** or **Comma (1.234,5)**. It only matters for a frequency with a fraction of a kHz, such as a spot at 14074.5.
8. Click **Test Connection**, then **Save**.

## Command sequences

Commander's TCP interface has no commands for some controls, but it can run a command sequence you build in its **Command Sequences** window.

Under **Commander command sequences (optional)** in the rig editor, enter a sequence's name, or `#3` for Commander's third sequence, next to the control it should run. That control then appears in POTACAT. A toggle, such as noise blanker on and off, needs both its on and its off sequence.

## Logging to DXKeeper

Controlling the radio through Commander and logging to DXKeeper are separate settings. To send POTACAT's QSOs to DXKeeper, see [Logbook Forwarding](logbook-forwarding.md).
