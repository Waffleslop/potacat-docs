# Hunter Mode

Hunter mode is the default view. It shows live spots from all your enabled sources in a sortable table and/or interactive map.

## Reading the spot table

### Worked-station indicators

| Indicator | Meaning |
|-----------|---------|
| ✅ | You've worked this station before — the call is in your POTACAT log. |
| Greyed-out row | You've worked this station **this UTC day** on the same band and mode. |
| Yellow star | The callsign matches your watchlist. |
| `NEW` badge | The park isn't on your worked-parks list yet. |
| `DXP` (red row) | DXpedition spot — pinned to the top of the table. |

Both worked indicators update automatically when you log a contact in POTACAT — there's nothing to sync from pota.app. Watchlist matches can also raise a corner flag and play a chime (enable in **Settings**).

> **Note:** The worked-today match also considers the park reference, so an activator who moves to a new park shows as workable again even if you worked them earlier in the day. Grey-outs clear at UTC midnight — a station you worked yesterday (UTC) turning white again is expected, not a bug.

### Spot-source pills

Every spot carries a pill identifying the network it came from (POTA, SOTA, DX cluster, and so on). When the same station is spotted by more than one source, POTACAT de-duplicates the spots into a single row carrying multiple badges (for example POTA + DX + CWops).

> **Tip:** Hover the FreeDV pill to see a countdown to the next poll — FreeDV spots come from a source that can only be polled about every five minutes.

### Multiple spots for the same callsign

If a station is spotted on more than one frequency, each spot stays in the table. POTACAT deliberately does *not* drop the older spot when a call is re-spotted elsewhere — otherwise a single bogus re-spot could knock a real activator off everyone's table. Two spots within `0.5 kHz` of each other highlight together as the same station. Use the hide options below to tidy up spots you don't want.

> **Tip:** The spot you've clicked to tune to is held on screen past its normal timeout, so the station you're working doesn't age out of the table mid-QSO.

## Skipping and hiding spots

### Skip

**Skip** marks a spot to be passed over — it's designed for Scan mode. Skips are tracked per **callsign + frequency**, kept in memory only, and reset when you restart POTACAT. A skip does not follow an activator who QSYs to a new frequency. Stations you've already worked today are auto-skipped during a scan; click **Unskip** to force one back in.

A **Hide** button next to Skip hides the station until they QSY to a new band.

### Right-click hide

Right-click any spot to hide it for **1 hour**, **2 hours**, **1 UTC day**, or **forever**. The hide applies to that callsign + frequency — not to everything from that call — and every hide can be reviewed (and undone) in the hidden-spots list.

### Hiding worked stations and parks

Three related checkboxes control worked-spot hiding:

| Option | Matches on |
|--------|------------|
| **Hide worked stations** | Callsign + UTC day + band + mode |
| **Hide worked parks** | Park reference (from your imported pota.app CSV) |
| **Hide worked call+park combos** | Callsign + park |

A hidden worked station reappears at the next UTC day **or** as soon as the activator changes parks. There's also a **Hide QRT spots** option, and a **Hide Worked Parks** quick toggle on the quick-access settings menu.

## Filters

- Uncheck bands you don't want in the **Band** filter dropdown (for example, to drop 2m/70cm spots).
- The **Mode** filter's **Radio** option is distinct from picking a fixed mode like **SSB** — selecting **SSB** shows only spots whose listed mode is SSB.
- Spots with no mode listed get their own filter category, so mode filters don't silently hide them.
- Spots can also be limited to your license-class privileges.

## Tracking new parks

Download your hunted-parks CSV from **pota.app → My Stats** and import it in **Settings**. POTACAT then flags parks you haven't worked with a `NEW` badge, and the **Hide Worked Parks** filter turns the table into a new-parks-only view.

You only need to import the CSV once: on startup it's merged with POTACAT's local worked-parks list, and every QSO you log appends its park reference(s) — POTA and WWFF — automatically. POTACAT Cloud subscribers also get automatic parks-worked sync. The stats overlay's "Unique Parks" and "Park QSOs" figures come from this parks-worked list, not from your lifetime QSO count.

> **Note:** The `NEW` badge reflects POTACAT's local worked-parks list, not your live pota.app account. POTACAT counts a park the moment you log it, while pota.app only *credits* a hunt after the activator uploads their log — so the two can disagree for a while.

> **Note:** Some users report that multi-state parks in the pota.app CSV appear only under the state where the park was first activated.

## Logging from the spot table

Ctrl-click (Cmd-click on Mac) selects multiple spots so you can log several operators in one pass — perfect for multi-op activations sharing one frequency. Hover the **LOG** button for a reminder of this.

> **Tip:** For a pass-the-mic pileup on a single spot, you can also comma-separate callsigns in the call field — POTACAT writes one log entry per operator. Comma-separating park references logs an n-fer hunt the same way.

Logging a POTA QSO automatically re-spots the activator unless you've turned re-spotting off.

## Special events and contests

POTACAT tracks special events and contests such as **13 Colonies**, **ARRL WAS 250**, and **CQ WW 160**, with a "What's Next" view of upcoming events. Event definitions are delivered server-side — POTACAT checks for active events at startup and every four hours — so new events show up without an app update.

For **13 Colonies**, a progress checklist tracks which special-event stations you've worked, and the JTCAT/FT8 views flag 13 Colonies calls you've already worked. In the mobile app, the progress chart shows the *last known spot* of each station you're still missing.

> **Note:** Event progress comes from QSOs logged in POTACAT — some users report that importing an ADIF does not update 13 Colonies progress.


