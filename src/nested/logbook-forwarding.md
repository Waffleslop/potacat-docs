# Logbook Forwarding

POTACAT can forward QSOs in real-time to external logging software:

| Logbook | Protocol | Default Port |
|---------|----------|:------------:|
| DXLab DXKeeper | TCP (Network Service) | 52001 |
| HamRS | WSJT-X binary UDP | 2237 |
| Ham Radio Deluxe | UDP ADIF | 2333 |
| Log4OM 2 | UDP ADIF (or WSJT-X binary) | 2237 |
| Logger32 | WSJT-X binary UDP | 2237 |
| MacLoggerDX | WSJT-X binary UDP | 2237 |
| N3FJP | TCP API | 1100 |
| Wavelog | HTTP API (URL + API key) | — |
| World Radio League | N1MM UDP protocol → WRL Cat Control | 12060 |

Enable in **Settings → Logging → Send Data to Logbook**. Select your logger and configure the host/port — picking a logger pre-fills its default port and shows setup instructions for that logger's side.

> **Note:** N1MM Logger+ itself is not a forwarding target — N1MM doesn't accept inbound QSOs this way. The "N1MM protocol" in the table is the transport WRL Cat Control listens with. To feed N1MM-centric workflows, forward to a logger that syncs with it.

## Remote Logging

The default IP address `127.0.0.1` only works when your logging software is running on the same computer as POTACAT. If your logger runs on a different machine on your network, enter that machine's IP address instead (e.g., `192.168.1.100`). Make sure the port matches what your logging software is listening on.

## Per-Logger Notes

### World Radio League

WRL's logging intake reads only the basic N1MM-style fields and discards the `SIG_INFO` and `POTA_REF` park fields that POTACAT sends with every QSO — so the park number survives only in the WRL comment field. A true park field in WRL would require a change on WRL's side. POTACAT includes the park tag in the WRL comment automatically, even when the park-in-comment option is turned off.

> **Note:** POTACAT's own ADIF log keeps the proper park fields, so your POTA exports are unaffected by this WRL limitation.

### DXKeeper (DXLab)

DXKeeper has no field literally named "POTA" — the park reference lands in the **SIG Info** column (`SIG_INFO`). POTACAT sends `SIG=POTA`, `SIG_INFO`, and `POTA_REF` (plus the `MY_` equivalents when you're activating).

> **Tip:** If you want a dedicated park column, create a DXKeeper user-defined item with a caption, then enable DXKeeper's option to import unrecognized ADIF fields by caption — `POTA_REF` will land there.

### N3FJP / ACLog

Forwarding relies on N3FJP's TCP API. In N3FJP, open **Settings → Application Program Interface** and check **TCP API Enabled**, port `1100` (the default). N3FJP must be running to receive QSOs.

> **Warning:** Some N3FJP installs (the Field Day edition, for example) leave the TCP API disabled. If forwarding silently stops working, check this setting first.

> **Note:** If you also run WSJT-X, launch order matters: start **WSJT-X** first, then **POTACAT**, then **N3FJP**.

POTACAT writes the park number and name into N3FJP's comments field. From v1.9.4 there is an option that controls whether POTACAT forwards comments, so you can turn this off if you prefer to keep your own comments.

### Log4OM 2

If forwarded QSOs aren't showing up, check that Log4OM's inbound UDP connection is enabled on port `2237` and restart Log4OM. POTACAT's verbose log will usually show the QSO going out — the problem is almost always on the receiving end (one confirmed cause: duplicate port numbers assigned inside Log4OM's connection settings).

> **Warning:** Duplicate-import trap: if Log4OM's ADIF Monitor watches POTACAT's ADIF file, any ADIF you *import into POTACAT* looks like new QSOs to Log4OM and gets re-imported. Pause the monitor during imports, do large imports before enabling the integration, or rely on Log4OM's duplicate detection (same call + date + time + band).

Log4OM treats plain ADIF UDP as a batch import and will **not** propagate those QSOs to QRZ or Club Log. To fix that, enable **Use WSJT-X binary protocol** in **Settings → Logging** — and in Log4OM, change the UDP Inbound entry's Type from "ADIF-MESSAGE" to "WSJT-X" (same port). Log4OM then treats forwarded QSOs like manually logged ones and uploads them normally.

### Wavelog

Enter your Wavelog server's base URL **without** `/index.php` on the end — including it causes a `404` and no QSOs arrive.

If Wavelog rejects a QSO with "You tried to import a QSO without any given Band," update POTACAT — older versions didn't derive the band when logging from the quick-log bar at the bottom of the table.

> **Tip:** A Wavelog "abort" in POTACAT's log usually means one of three things: the wrong station profile ID, an API key that lacks permission for that profile, or a frequency outside a known band.

### MacLoggerDX

MacLoggerDX only accepts the WSJT-X binary protocol — POTACAT forwards to it in that format on UDP port `2237` (plain ADIF does not work). To get POTA and SOTA references into MacLoggerDX, enable its **WSJT-X Log ADIF** setting, found under the Log section of MacLoggerDX's preferences.

> **Tip:** RUMlogNG users report the same path works for them: select **MacLoggerDX** as the target in POTACAT, then in RUMlogNG enable **Preferences → UDP → WSJT-X → Save QSOs to logbook** with data port `2237`.

### HAMRS

POTACAT sends the park reference in `POTA_REF`, `SIG_INFO`, and `SIG=POTA` over the WSJT-X UDP protocol, but HAMRS writes it only into the Comments field — HAMRS's "Their Park" field stays empty. This is a limitation on the HAMRS side (a feature request has been filed with HAMRS).

### QRZ Logbook

Some users report that a QRZ password containing a `%` character breaks the QRZ login from POTACAT — and from QRZ's own site. This is an issue on QRZ's side; if your login fails, try a password without `%`.
