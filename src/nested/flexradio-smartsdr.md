# FlexRadio (SmartSDR)

**Best for:** FlexRadio 6000/8000 series running SmartSDR.

POTACAT connects to SmartSDR's built-in CAT server over TCP. No additional software or cables needed.

1. In SmartSDR, make sure the **CAT server** is enabled (SmartSDR CAT settings)
2. Add a new rig → select **FlexRadio (SmartSDR)**
3. Choose your slice (A, B, C, or D)
4. Save

SmartSDR exposes Kenwood-compatible CAT on TCP ports 5002–5005:

| Slice | Port |
|-------|------|
| A     | 5002 |
| B     | 5003 |
| C     | 5004 |
| D     | 5005 |

If SmartSDR is on a different computer, use **IP Radio (TCP CAT)** instead with the Flex's IP address.

> **Tip:** Start order matters. If spot clicks or QSY start erroring, close both apps and reopen **SmartSDR first, then POTACAT**.

## Direct connection — SmartSDR doesn't have to stay open

POTACAT also binds directly to the radio's own API (TCP port **4992**), so SmartSDR isn't required to keep operating. If SmartSDR closes, POTACAT re-binds directly to the Flex within a couple of seconds, and hands back when SmartSDR reopens. CW is fully supported on this path, including keying through a **WinKeyer**.

## The "independent slice" gotcha

If **Run independent slice** is checked in the rig settings, clicking spots will **not** move your SmartSDR slice — POTACAT works its own slice instead, and on some radios that means a brand-new slice opens (e.g. slice C on a 6600). If spots show up but the radio never QSYs, **uncheck it**.

## Digital and remote audio need DAX

ECHOCAT and JTCAT audio go through SmartDAX, not the CAT connection:

1. **DAX must be running.**
2. In SmartSDR, assign the slice flag to a **DAX channel**.
3. The SmartDAX window should show a **blue** indicator next to that slice.
4. In POTACAT, select the **DAX Audio RX/TX** devices as the rig's audio in/out.

There's also a setting to pin your TX to a chosen **DAX channel**, so transmit audio never silently loses its DAX assignment.

## JTCAT / FT8

JTCAT talks to the SmartSDR API host on TCP port **4992**. Make sure POTACAT has the Flex's IP address configured — it's the same address used for [SmartSDR panadapter spots](smartsdr-panadapter-spots.md) — and that your firewall allows **POTACAT** to reach the radio. A firewall rule that only allows SmartSDR.exe isn't enough.

## Tuner Memories (internal ATU)

From POTACAT 1.13.9, **More ▾ > Tuner Memories** fills your Flex's own antenna tuner memories for every band and mode you use. POTACAT tunes to each point, lets the radio's tuner find a match and stores it in the radio, so a later band change recalls the match instead of running a tune cycle.

- It appears in the **More ▾** menu only when the radio is connected with **Flex Direct** and has an internal ATU.
- The window walks you through it: check that the antenna is connected and no amplifier is inline (or it's in standby); tick your **Bands and modes**; set the **Tune power** (25 W at most), the **SWR that counts as matched**, and what to do **If a frequency is busy**; add **Your own frequencies** if you like; then **Review the plan** and run it.
- The radio transmits a low-power carrier for about a second at each point, and listens first. The plan stays 3 kHz inside the edges of the license class set in Settings and never transmits outside it.
- **STOP** ends a run at any time. **Results** shows each point; **Run verification pass** re-checks them and **Export CSV** saves them.
- Bands where no match was found are hidden in the rig editor, with a note saying the last Tuner Memories run hid them.

## Connection troubleshooting

If POTACAT suddenly can't connect (often after an upgrade), test from PowerShell:

```powershell
Test-NetConnection <radio-ip> -Port 4992
```

- **True**, but POTACAT still fails → your firewall allows SmartSDR.exe but not POTACAT.exe, or the radio has hit its multi-client limit (default: 2 GUI clients). Close an extra client and retry.
- **False** → your PC is on the wrong subnet from the radio.

## See also

- [SmartSDR Panadapter Spots](smartsdr-panadapter-spots.md) — push POTA/SOTA/DX spots onto your panadapter, including on Maestro and SmartSDR for iOS.
