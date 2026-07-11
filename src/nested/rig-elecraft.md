# Elecraft K4, K3S, KX2 & KX3

Elecraft rigs speak a Kenwood-derived protocol, but each model has its own quirks — and picking the exact **Radio Model** in POTACAT's rig settings is what makes them behave.

## K4 / K4D

### Pick the K4 model

Select **K4** explicitly as the Radio Model. The K4 uses Elecraft's `DT` data sub-mode commands rather than the Kenwood ones: for FT8/DIGU POTACAT sends **`MD6` (DATA) + `DT0` (DATA-A)**, and **`MD9` (DATA-REV)** for DIGL. With a generic profile the radio lands in the wrong data variant, so the model selection matters.

### Network CAT and remote operation

- For remote control over the network, use the **K4 Remote (network)** connection type (distinct from the generic **IP Radio (TCP CAT)**): enter the K4's IP or hostname, port **`9205`** (plain TCP), and the **remote password** you set on the radio.
- Port `9204` (TLS-PSK) is **not** supported — use `9205`.
- POTACAT performs the K4's authenticated handshake and keeps the session alive with a heartbeat. A wrong password shows up in the log as `socket closed before session established`.

### SWR bar stays empty

The K4 rejects the K3-era `RM1;` SWR query, so POTACAT doesn't poll SWR on the K4. An empty SWR bar is normal on this radio.

> **Tip:** If the bandwidth looks wide after clicking a spot, check the K4's own per-mode bandwidth defaults — that's usually the radio's stored setting, not POTACAT.

## K3 / K3S

If CW spot clicks land you in a wide filter, two rig-side settings are responsible:

1. **CONFIG > RX BW LOCK** must be `OFF`. When bandwidth is locked, the K3 silently ignores the `FW` (filter width) commands POTACAT sends.
2. The per-mode **filter bank** (the **FB** button) must have a narrow roofing filter (250/500 Hz) selected for CW. POTACAT sends only `FW` — the DSP width — and never `FB`; the roofing filter choice is something you set once on the rig, and `FW` can only narrow within it.

> **Tip:** Set your preferred per-mode filter widths in **Settings > Tuning** and they'll persist across spot clicks and band changes.

## KX2 / KX3

- Both work out of the box over **Serial CAT (Kenwood)** at `38400` baud.
- **FT8/JTCAT**: the KX-series per-band memory recall can override DATA A when you change bands. Set the Radio Model to **KX2/KX3** so POTACAT re-sends the mode after each QSY.
- The K3 filter-width advice above applies here too: set per-mode widths in **Settings > Tuning**.
