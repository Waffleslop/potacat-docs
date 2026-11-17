# FreeDV / PSKReporter

FreeDV spots from PSKReporter. Polls every 5 minutes (with automatic backoff on server errors). Coral-colored spots in the table and map.

Hover over the FreeDV checkbox in the Spots dropdown to see a countdown to the next poll.

## Settings

In **Settings > Spots**:

- **FreeDV (PSKReporter)** turns on live FreeDV reception reports from PSKReporter.
- **Report my JTCAT decodes to PSKReporter** sends what JTCAT decodes to PSKReporter every 5 minutes. It needs your callsign and grid, and has an optional **Antenna** field.

The **Propagation** view (**More ▾ > Propagation**) has its own **PSKReporter** toggle, and its PSKReporter map is on by default.

FreeDV Reporter (qso.freedv.org) is a spot source too. Its spots carry the same **FreeDV** badge.

FreeDV digital voice itself is a separate setting, **FreeDV Digital Voice**, in **Settings > Station**.

## FreeDV Digital Voice (receive)

This section describes POTACAT 1.14.6.

1. Tick **FreeDV Digital Voice** in **Settings > Station**.
2. Click a FreeDV spot, or pick **RADE** in the VFO window's mode list.

- **Receive only.** FreeDV transmit is not built yet. PTT is off in FreeDV modes, from every surface, so ordinary voice is never sent on a FreeDV frequency. Pressing PTT in ECHOCAT does not key the radio, and the app says *FreeDV transmit is coming in a later update, so PTT is off in FreeDV modes. Tune to an SSB frequency to talk.* FT8, SSTV, Winlink and Tune still key.
- **Windows, Mac and Linux.** FreeDV (700D, 700E, 700C, 1600) and RADE V1 decode on all three. Mac (Apple Silicon and Intel) and Linux are new in 1.14.6, so reports of how it sounds on the air are welcome.
- **On Windows,** receiving RADE V1 before 1.14.6 closed POTACAT at the end of each over. It now plays the whole over at the right speed.
- **ECHOCAT and ECHOCAT Web hear the decoded speech,** at about the level of SSB audio. Starting FreeDV from ECHOCAT starts it on the shack.
- **Known:** a few seconds after you pick RADE, the VFO window's mode badge shows **USB**, which is the radio's mode. The decoder keeps running.
