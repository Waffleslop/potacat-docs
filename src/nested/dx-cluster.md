# DX Cluster

Live DX spots streamed via telnet from DX cluster nodes. POTACAT supports up to **3 simultaneous cluster connections**.

**Setup:**
1. Enable DX Cluster in Settings → Spot Sources
2. Enter your callsign (required for cluster login)
3. Choose from 13 preset nodes (W3LPL, VE7CC, DXUSA, NC7J, K1TTT, and more) or add a custom node
4. Optionally add a second and third node for broader coverage

DX Cluster spots appear with a purple left border in the table and purple markers on the map. Location is resolved from the callsign using the bundled cty.dat country database.

**DX Command Bar:** When DX Cluster is enabled, a command bar appears below the table. Use it to self-spot or spot other stations on the cluster. Enter a callsign, frequency, and optional comment, then click Send.

**Spotting on the cluster:** The Log dialog includes a "Spot on DX Cluster" checkbox for non-park contacts. Press **Ctrl+R** for quick re-spotting with template variables.

---

## Maximising your S50CLX DX Cluster experience

*Contributed by Dan, S50U — sysop of [S50CLX](https://s50clx.si).*

The examples below use S50CLX (running DXSpider), but the same commands work on any DXSpider node.

### Let the cluster do the heavy lifting

For best performance, offload filtering to the node you are connected to (S50CLX in our case) over telnet. Configure the node to deliver only the spots relevant to you, instead of letting your logging software filter unwanted data after it arrives. This saves your computer's processing power and reduces unnecessary bandwidth for both you and the network.

### Persistent user profiles

The first time you connect to S50CLX, it automatically creates a user account tied to your callsign. This account stores all your preferences, so any adjustments you make remain active until you change them. Once logged in, set your details so others can find out who and where you are:

```
set/name Dan
set/qth Cerkno
set/qra JN66WD
set/home S50CLX
```

### Tailoring your connection with SSIDs

Different operating scenarios — contests, casual DXing, POTA hunting — call for different filtering. SSIDs let you keep multiple, independent configurations under the same callsign. An SSID is simply a suffix added to your callsign (e.g. `S50U-1`). The node treats each SSID as a distinct user, with its own filters and commands, all of which persist across sessions. The SSID is stripped from any spots you originate, so it never appears in the wider cluster feed.

A few practical examples:

- `S50U-1` — only CW spots from NA-based stations
- `S50U-2` — all HF SSB CONTEST spots across Europe
- `S50U-3` — only spots whose comments contain POTA or SOTA references

You can have up to 99 SSIDs (1–99).

### Simultaneous connections

Without an SSID, the node permits only one active session per callsign — a second login would disconnect the first. Assign a unique SSID to each connection (e.g. `S50U-1` from your laptop, `S50U-2` from your shack PC) and you can stay logged in across all your devices at once.

### Mastering filters for precision spotting

Filters give you fine-grained control over the spot stream. For example, to receive spots only from spotters in CQ Zones 14, 15, 16, and 20:

```
accept/spots by_zone 14,15,16,20
accept/rbn by_zone 14,15,16,20
```

Or only from North American spotters:

```
accept/spots by_zone 3,4,5
accept/rbn by_zone 3,4,5
```

Filters can be as simple or as sophisticated as needed and support full boolean logic. A comprehensive guide is on the [DXSpider Filtering Manual](https://www.dxcluster.org/main/usermanual_en-13.html) page.

Note that standard spots and Reverse Beacon Network (RBN) spots are managed separately, so you'll need to apply filters to each stream individually.

### Essential filter commands

Each callsign+SSID combination can hold up to ten accept and ten reject filters for both regular and RBN spots:

```
reject/spots <0-9> pattern
accept/spots <0-9> pattern
reject/rbn   <0-9> pattern
accept/rbn   <0-9> pattern
```

Patterns can include:

- Frequency ranges (`freq`, `on`)
- Text strings in comments (`info`)
- Callsign prefixes (`call`, `by`)
- DXCC, ITU, or CQ zone numbers (`call_dxcc`, `by_itu`, `call_zone`)
- US state abbreviations (`call_state`, `by_state`)

### Handy cluster commands

- `sh/filter` — display all active spot and RBN filters for your current SSID
- `sh/dx` — list the ten most recent spots; add a number, e.g. `sh/dx 50`, to see more
- `sh/dx <callsign>` — recent spots for a specific callsign (e.g. `sh/dx S5` for Slovenian stations)
- `sh/muf <prefix>` — current Maximum Usable Frequency to a given country, with band-by-band signal strength estimates over time
- `sh/prefix <callsign>` — country information for any callsign
- `sh/users` — everyone currently connected to the node

### Getting the most from the RBN

Enable all-mode RBN spots (the data volume is enormous):

```
set/skimmer
```

Disable with:

```
unset/skimmer
```

You can also target specific modes:

```
set/skimmer cw
set/skimmer rtty
set/skimmer ft
set/skimmer cw rtty
```

While RBN servers broadcast every report they receive, the cluster software intelligently filters out erroneous and duplicate entries — saving bandwidth and giving you a cleaner, more reliable spot feed.

### Monitoring your own spots

```
set/seeme
```

This shows every spot of your own callsign as it appears in the cluster, **before** any filters are applied. An excellent way to see where and when you're being reported worldwide in real time.

### Unlock the full potential

This is only the surface of what's possible with an S50CLX cluster node. Diving deeper into filtering, SSIDs, and the full command set lets you tailor the cluster to work exactly the way you want.

*April 2026 — Dan, S50U, sysop of S50CLX ([s50clx.si](https://s50clx.si))*
