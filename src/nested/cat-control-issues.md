# CAT Control & Test Connection

This page is for when CAT control *isn't* working — Test Connection fails, spot clicks stop tuning the radio, or CAT dies mid-session. For first-time setup, start with [Radio Setup](../radio-setup.md) and the page for your connection method, such as [Other Rig (Hamlib)](other-rig-hamlib.md) or [Serial CAT (Kenwood)](serial-cat-kenwood.md).

## First checks

Two settings cause a surprising share of "CAT is broken" reports:

1. **Rig Model dropdown** — picking a connection type isn't enough. The **Rig Model** dropdown in the rig editor must be set to your exact radio so POTACAT can apply that model's quirks. With a generic or empty model, tuning can silently fail, and some radios beep continuously as they reject commands they don't understand.
2. **Enable Split Mode** — if your radio unexpectedly jumps to VFO B or switches split on when you click a spot, check whether **Enable Split Mode** is turned on in Settings and turn it off.

## Test Connection fails

Work down this checklist — it resolves the vast majority of failed tests:

| Check | Details |
|-------|---------|
| **Baud rate** | The baud rate in POTACAT must exactly match the CAT rate set in your radio's menu. A mismatch usually looks like a silent timeout or `read ECONNRESET`. Some radios (Kenwood, for example) need a power cycle after you change the baud in the rig menu. |
| **Which COM port?** | Many radios — especially Yaesu with the Silicon Labs CP210x driver — expose **two COM ports** over one USB cable. Use the **Enhanced** port for CAT. If the first port fails, test the other one. Check **Device Manager > Ports (COM & LPT)** to see both. |
| **VFO A selected** | Make sure the radio is sitting on **VFO A** before you test. Some rigs misbehave when CAT commands arrive while VFO B is active. |
| **Virtual COM ports** | Ports created by virtual serial port software don't appear in the dropdown — **type the port name manually**, e.g. `COM15`. Typing the bare port name (e.g. `COM7`) instead of accepting the auto-detected dropdown entry has also fixed "test passes but nothing tunes" cases. |
| **DTR/RTS** | Toggle **Disable DTR/RTS on connect** and test again. USB adapters differ — some need it checked, others need it unchecked. |

## The CAT fight

**Only one program can own a serial port at a time.** If a logger or digital-mode app is already holding the radio's COM port, POTACAT's test fails — often with "Access denied" — or CAT drops the moment the other app polls the radio.

- Turn off CAT/rig control in your logger (N3FJP, Ham Radio Deluxe, Log4OM, and similar) and let POTACAT own the port.
- Close WSJT-X, FLRig, and any other CAT software before testing.
- If you want other apps to share the radio, point them at POTACAT's rigctld instead of the COM port — for example, configure WSJT-X to use **Hamlib NET rigctl** at `127.0.0.1:4532`, and open POTACAT first.

## The WSJT-X Mode trap

This is the single most common cause of "CAT suddenly stopped working."

Clicking the **CAT** pill in the top bar reveals a **WSJT-X Mode** checkbox. When it's on, **POTACAT no longer controls your radio at all**. Instead, it sends frequency changes to WSJT-X over UDP, and WSJT-X does the CAT work. That's why the CAT pill turns red (or reads "WSJT-X"), the CAT log is empty, and spot clicks and PTT do nothing — even though nothing is "broken."

If you enabled WSJT-X Mode without WSJT-X actually running, you've handed rig control to a program that isn't there.

- **Option A — direct control (recommended for most hunting):** uncheck **WSJT-X Mode**. POTACAT tunes the radio itself. This is the right choice for SSB/CW POTA hunting.
- **Option B — keep WSJT-X Mode:** make sure WSJT-X is actually running and listening on UDP port `2237`, with its rig configured as **Hamlib NET rigctl** at `127.0.0.1:4532`. Open POTACAT first, then WSJT-X, then your logger — this order avoids the CAT fight.

> **Note:** For FT8 inside POTACAT, use JTCAT with WSJT-X Mode **off**. Don't run JTCAT and WSJT-X against the radio at the same time.

## Which CAT path am I on?

Three of POTACAT's connection methods are easy to mix up:

| Method | How it works | Use it when |
|--------|--------------|-------------|
| **Other Rig (Hamlib)** | POTACAT spawns its own bundled `rigctld` process and translates to your radio's native protocol | Most serial-connected radios — see [Other Rig (Hamlib)](other-rig-hamlib.md) |
| **rigctld Network** | POTACAT connects to a `rigctld` that is *already running* — one you started yourself or one managed by other software | Sharing one radio between apps, or when software like deskHPSDR runs its own rigctld — letting POTACAT spawn a second one causes conflicts |
| **IP Radio (TCP CAT)** | Direct TCP connection to a radio or server that speaks Kenwood-style CAT over the network | FlexRadio slices, Elecraft K4, Thetis, and similar network radios |

### rigctld port conflicts

When you use the Hamlib path, POTACAT's internal rigctld listens on port **4532**. If other software also runs rigctld on 4532 (Log4OM can, among others), the two collide — POTACAT may fail to connect or even control the wrong radio. Fix: set the **rigctld Port** field in the Hamlib rig editor to any unused port, e.g. `4534`.

## FLRig

POTACAT can use FLRig as its CAT layer, which is handy for radios that behave better under FLRig:

- In the rig editor, type FLRig's address into the COM-port field — FLRig's XML-RPC server listens on port `12345` by default, so this is typically `127.0.0.1:12345`.
- Alternatively, bridge it yourself: run `rigctld -m 4 -r 127.0.0.1:12345` (Hamlib model 4 is FLRig), then add the rig in POTACAT as **rigctld Network** pointing at `127.0.0.1:4532`.

> **Note:** Port `4532` belongs to rigctld, not FLRig. Don't point a FLRig entry at 4532.

## Win4Yaesu / Win4Icom middleware

Some users report that CAT routed through a Win4Yaesu or Win4Icom virtual COM-port chain **silently drops after transmitting** — the CAT indicator stays green, but the radio stops following spot clicks until the rig is re-selected. If you don't need the middleware, **connect POTACAT directly to the radio's COM port**. If you do need to share the radio with Win4Yaesu, see [Win4Yaesu Setup](win4yaesu-setup.md).

## Where settings live (and factory reset)

POTACAT's settings are stored outside the app, so they survive updates — and uninstalls. That means uninstalling and reinstalling will *not* fix a corrupted configuration. To reset to a first-run state, delete the settings folder:

| Platform | Location |
|----------|----------|
| Windows | `C:\Users\<you>\AppData\Roaming\POTACAT` |
| Linux | `~/.config/potacat` |

> **Warning:** Deleting this folder wipes all settings, rig configurations, and cached data. Use the settings **export** option in Settings first if you want a backup to restore from.

## When an update goes wrong

- Press **F5** inside POTACAT to fetch the latest update.
- If **Restart to Update** hangs or loops, open Task Manager and kill the **POTACAT Launcher** process, then retry the update.
- To roll back a bad release, every GitHub release includes a **portable .exe** in its assets ([github.com/Waffleslop/POTACAT/releases](https://github.com/Waffleslop/POTACAT/releases)). It runs standalone — no uninstall needed — and picks up your existing settings.
