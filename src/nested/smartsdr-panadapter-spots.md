# SmartSDR Panadapter Spots

For FlexRadio users: enable **Push spots to SmartSDR panadapter** in Settings → Display. POTACAT connects to the FlexRadio API on port 4992 and displays color-coded spot markers directly on your SmartSDR panadapter.

Configure which sources appear (POTA, SOTA, DX Cluster, RBN, etc.) and set a max spot age.

Spots appear on every SmartSDR client — Windows, iOS, and Maestro.

> **Tip:** Run POTACAT on an always-on shack PC and the spots stay on the panadapter for every remote client (e.g. a Maestro or iPad). Avoid running two POTACAT instances against the same radio at once. Some users find a panadapter must be left open on the host SmartSDR for spots to reach remote clients.

## How it works (protocol)

POTACAT opens a plain TCP connection to the SmartSDR API on port **4992** — the same port SmartSDR itself uses; the radio accepts multiple simultaneous clients. Commands are ASCII text, newline-delimited, in the form `C<seq>|<command>`:

```text
spot add rx_freq=7.074000 callsign=W5XYZ mode=CW color=#FF4ECCA3 source=POTACAT trigger_action=tune lifetime_seconds=600 comment=Some_note
spot remove callsign=W5XYZ source=POTACAT
spot clear
```

Useful if you want to script your own spot pushes or understand what POTACAT is doing on the wire.
