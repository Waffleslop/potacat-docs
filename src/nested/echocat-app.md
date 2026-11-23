# The ECHOCAT App: What It Has Today

This page describes the ECHOCAT phone app as released on 21 November 2026: version 1.5.x on iPhone and Android, with the over-the-air updates through 20 November 2026. The latest POTACAT desktop on that date is 1.14.7.

Most of the app is a remote view of POTACAT on your shack computer. Where a feature needs a certain POTACAT version, the line says so; on an older desktop the feature is hidden or shows nothing.

For pairing and connection paths, see [ECHOCAT](../echocat.md) and [Connectivity & Pairing](echocat-connectivity.md).

## Updates

- App updates arrive over the air for version 1.5.0 and later. An install older than 1.5.0 gets none; update it from the store.
- When an update is ready, a card at the top of **Settings** reads *An update is available* and *Tap here to install it. ECHOCAT restarts in a few seconds.* While you transmit it reads *It installs when you stop transmitting.*
- A new store version gets a one-time card on Spots.
- **Settings > Help > About** has **Check for updates**, and shows the version line with the update's id. Tap the line to copy it.

## Settings

From the over-the-air update of 23 November 2026, Settings is in six groups. Nothing was removed; some options are one level deeper. This guide uses the new paths.

- **Search settings**, at the top, finds any option. The old row names work as search words, so typing an old name still finds it.
- The callsign card under it shows your callsign, grid, connection, radio and shack computer. Tap it to open **Operator**.
- **Station:** Connection, Rig, Paired desktops, Audio, Bluetooth PTT button, Idle Mode.
- **Finding stations:** Spots, Watchlist, Scan, SDR receivers.
- **Modes:** Voice macros, CW, Digital modes, SSTV, Winlink.
- **Look & feel:** Appearance, Layout.
- **Account:** POTACAT Cloud, Guest Pass, Redeem a pass, Privacy & data.
- **Help:** Diagnostics, Send feedback, About.

Some rows show only when they apply: Connection and Bluetooth PTT button need a newer store version, Idle Mode shows when the desktop takes it from the phone, and Winlink shows with the Mail tab.

Where the common ones went:

| Before | Now |
|---|---|
| Hardware > CW keyer, Operating > CW | **Modes > CW** |
| Operating > JTCAT (FT8/FT4) | **Modes > Digital modes** |
| Operating > Audio levels (TX Drive, RX Boost, RX Level, EQ, compressor) | **Station > Audio** |
| Hardware > Audio bridge | **Station > Audio** |
| Hardware > Rig, Paired desktops | **Station** |
| Hardware > SDR Receivers | **Finding stations > SDR receivers** |
| Operating > Spots, Watchlist, Scan | **Finding stations** |
| Operating > Watchlist groups | **Finding stations > Watchlist > Watchlist groups** |
| Operating > SSTV, Winlink; Hardware > Voice macros | **Modes** |
| Operating > Distance | **Look & feel > Appearance > Distance** |
| App > Appearance, Layout | **Look & feel** |
| Account > Manage Account, Last Sync, API keys | **Account > POTACAT Cloud** |
| Account > Shared rigs | **Account > Guest Pass > Shared rigs** |
| Help > Rate ECHOCAT | **Help > About > Rate ECHOCAT** |
| Operating as (card at the bottom) | The callsign card at the top |

## Appearance

**Settings > Look & feel > Appearance.** Choose the mode first (**System**, **Light** or **Dark**), then a theme for that mode. A new install starts on System. **Distance** (miles or kilometers) is on the same screen.

- Dark themes: **POTACAT Dark** (the default), **Midnight**, **Acid Burn**, **Miami Nights**. Acid Burn sets all text in a monospaced font.
- Light themes: **POTACAT Light**, **She's On Frequency**.

These are the same six themes as POTACAT desktop from 1.14.4.

## The Header and Your Shacks

- The connection tag reads **LAN**, **CLOUD** or **TAIL**.
- With two or more paired shacks, tap the tag. A **Shacks** sheet lists them, with *CONNECTED* on the current one and **SWITCH** on the others. This needs POTACAT 1.14.2. A Cloud-only pairing made before 9 November 2026 may need to be paired again once.
- To remove a shack, long-press its row under **MY SHACKS** and confirm.
- While on Cloud or Tailscale, the app checks for the shack's home network every 30 seconds, and at once when the app comes back to the front, and moves to LAN when it answers. It waits if you are transmitting.
- When WSJT-X Mode is on at the shack, the app shows the banner *WSJT-X Mode is on at the shack* in place of *Radio offline*, and the CAT dot in the header turns amber; tap the dot to bring the banner back. The phone cannot turn WSJT-X Mode off. See [WSJT-X](wsjt-x.md).
- On narrow screens the ping readout is hidden and the frequency is sized to fit, so the Settings gear stays on screen.

## Spots and Map

- With the Long row layout, the callsign stays pinned on the left and the middle columns slide sideways together under a column header. When everything fits, nothing scrolls.
- Frequencies in MHz show with dots between the digit groups.
- The Spots map tints the states you have worked and confirmed, and Hunt has a wanted-state choice. This needs POTACAT 1.13.2.
- The map loads without the internet.
- The Log sheet from a spot has **+ Add second operator**, then **+ Add another operator**, with no limit. The button becomes **Log N QSOs**. Each operator is logged as a separate contact, and only the first one re-spots.

## Digi (FT8, FT4 and More)

The tab is labelled **Digi**. It opens on your last band and mode, with **Start** under it.

- **Band and mode** are picked in one sheet. While decoding, taps in the sheet only pick, and a **Switch to** *mode* **on** *band* button applies both in one cycle.
- **Clear** empties the decode list. Changing mode clears the decodes, the calling list and the waterfall.
- A cycle you transmitted in is headed *TX CYCLE*.
- **TX slot.** After **Hold TX**, a control cycles **Slot: Auto**, **Slot: 1st**, **Slot: 2nd**, for FT8, FT4 and FT2. If you call a station in the locked slot, an alert offers **Keep locked** or **Unlock and call**. Needs POTACAT 1.13.3.
- **Hunt targets** include **Anyone calling CQ**, **New countries**, **DX only (other continents)**, **Same as Call**, **Watchlist**, **POTA** and **SOTA**. Needs POTACAT 1.13.10.
- **Hunt filters.** A **Filters** pill opens the Filters sheet, and the status line sits under Hunt. Long-press a decode for **Never answer** *call*, or **Answer** *call* **again**. Needs POTACAT 1.14.0. Not shown on Local Rig or to a Guest Pass. See [Hunt filters](jtcat.md#hunt-filters).
- **Wanted states.** State badges on decodes are off to start. Turn them on in **Display > Wanted states**.
- **The shack's clock is off?** A banner has **Use this phone's time**. The desktop then corrects its FT8 timing from the phone and measures again every 10 minutes. Needs POTACAT 1.13.4.
- An FT8 transmit refused because the radio is on another band offers **Follow the radio**. Needs POTACAT 1.13.9.
- **Not on the phone:** the *Not logged* notice and **Send 73** button for a contact that ended before any 73. Use ECHOCAT Web or the JTCAT window. See [When a contact is logged](jtcat.md#when-a-contact-is-logged).

**Settings > Modes > Digital modes** has two more:

- **Keep screen on:** **Never**, **Scanning or decoding** or **Whenever connected**. Scanning or decoding covers Scan, FT8, FT4, FT2, WSPR, PSK, JTTY and JS8. The phone sleeps as usual once it loses the shack.
- **JTTY alerts:** **Off**, **My call** (the default) or **Any message**. You get a toast in the app, or a notification when you are on another tab or in another app. On an iPhone, alerts in the background need Audio on.

**JS8** has an **Inbox** / **Activity** switch. Activity lists every decoded frame, heartbeats included. Tap a row to open its thread.

**WSPR:** the band list includes 2 m. Idle Mode offers 2 m only when the shack's radio lists 2 m, and needs POTACAT 1.14.0.

## Pan (Panadapter)

A tab labelled **Pan**, for radios that send a band scope to POTACAT. It shows a full-screen scope and waterfall, a tuning card, a swipe strip for tuning, and a PTT button (**Key** and **Stop** in CW).

- Drag to tune. Tap the tuning card for the keypad.
- A FlexRadio panadapter and the FT-710 scope need POTACAT 1.13.6. Icom scopes need 1.13.7.

On the **VFO** tab, the scope section is called **Waterfall**. It shows the radio's own scope where there is one, otherwise the receive-audio waterfall.

## Radio Controls

- **Split.** Rig Controls has a **SPLIT** section with a **TX, VFO B** row, offset chips (**-1k**, **+1k**, **+5k**, **+10k**) and a TX frequency keypad. Offsets are from the receive frequency. The VFO tab shows a TX line and a SPLIT tag. Needs POTACAT 1.13.9. An IC-7300 with firmware older than 1.30 cannot set VFO B.
- **Rig presets** are on the VFO tab. When the desktop applies one, the phone shows a notice titled *Rig preset* and its name, with what changed. Needs POTACAT 1.13.0.
- **ATU.** The tune button lights only while the tuner is sweeping.
- **A radio with no CAT,** keyed by its sound card, gets the PTT button, and the *Radio offline* banner is hidden for it.
- **PTT release** ends with a 150 ms tail before the radio unkeys, so a radio that switches to DATA mode on key-down no longer clips. Safety releases are still immediate.
- A tune from Spots, Dir, Map, Pan, the VFO keypad or Act while an SSTV picture is being received asks before taking the radio.

## Dir (Directory)

The **Dir** tab has **HF Nets**, **SWL**, **Landmarks** and **Channels** pills. Needs POTACAT 1.13.8.

- A row your radio cannot hear but an SDR can carries an SDR tag. When an SDR takes over, the listening banner reads *Radio can't reach this · TX off*.
- A channel shows the radio memory number it recalls. Memory recall needs POTACAT 1.14.3.

See [Directory](directory.md).

## Act (Activations)

The tab is labelled **Act**. See [Activator Mode](../echocat.md#activator-mode) for the basics.

- **County.** At a US park, the running activation card has a County row. Tap it to pick the county, after the state when the park spans several. The choice goes in each contact as your own state and county.
- **Recap.** A recap sheet with a map and stats opens when you end an activation, and on a long-press of a past activation. **Share image** (iPhone) or **Save image** (Android) exports it as a picture. The map draws without the internet.
- **ADIF export** for POTA names files `CALL@PARK-YYYYMMDD`, one file per park, dated by the first contact.
- **Activation ended.** When the desktop ends a forgotten activation, at the UTC day change or after 6 hours with no contacts, the phone shows a toast titled *Activation ended*. Needs POTACAT 1.14.2.
- **With no signal:** unlocking the phone no longer rebuilds the shack link, and the app does not lag. The Log button keeps a copy of each contact on the phone even while connected. The phone's contacts are cleared only by your own Sign out.

## Logbook

- **Awards** opens a full-screen sheet with **WAS** and **DXCC** tabs. The name column is pinned, the band grid scrolls sideways, and a band picker narrows it. Needs POTACAT 1.13.3.
- FT4, FT2 and JS8 contacts show their real mode.

## SSTV

- The template browser has a read-only **FROM DESKTOP** section.
- Templates are saved in stages, with **CQ**, **Reply** and **73** chips and counts. Reply templates use THEIR CALL and REPORT fields. Saving templates to the shack needs POTACAT 1.14.6.
- A 73 card on the SSTV screen opens Compose and does not transmit.
- The text editor has typeface, outline, shadow and letter spacing. Needs POTACAT 1.14.3.
- The control bar has an ATU button, hidden while sending.

See [SSTV](sstv.md).

## Mail (Winlink)

A **Mail** tab with the folders **In**, **Out**, **Sent** and **Archive**. Needs POTACAT 1.13.1. See [Winlink Email](winlink.md#from-your-phone-or-a-browser).

- Account setup is in **Settings > Modes > Winlink**. With no password saved, the Mail tab opens on *Set up your Winlink account*.
- The composer queues with **Put in Outbox**. **Send / Receive** on the Mail tab is what transmits.
- The send sheet has **Send via**, **FAVORITES** (starred gateways, kept per frequency), **RADIO DIAL**, **Refresh** and **History**. Favorites and History need POTACAT 1.14.4.
- When the channel is busy, a card shows the shack's wait and has **Call anyway**, with the line *Call anyway only if you have listened and it is clear.*
- The tab shows the radio's own waterfall when the radio sends a scope.
- While the tab is open the radio stays on the gateway. Needs POTACAT 1.14.6.
- **Not on the phone:** an Archive button, a Deleted folder, Restore, Reply all, a Cc field and Winlink forms. You can read archived mail in the Archive folder. Use ECHOCAT Web or the desktop for the rest.

## Guest Pass

Needs POTACAT 1.14.6 for the parts below; an older desktop keeps the older behaviour. See [Share Your Rig](../echocat.md#share-your-rig).

- A guest sees one banner and card saying whether they are on the air, waiting, reconnecting, or the pass is over. Only an ended pass ends the session.
- The card's buttons are **Leave**, **Use it here instead**, **Take the radio**, **Stop** and **Close**. When the owner has been idle, the guest is told *Press Take the radio to go back on the air.*
- Notifications report the changes.
- A guest can listen on the station's SDRs and stop them, nothing else.
- On the owner's side the button is **Cancel pass**.
- When you make a Guest Pass on an account with two or more shacks, you pick the shack.

## Special Events

When POTACAT announces a special event, a one-time popup headed *POTACAT EVENT* appears, with a tracking choice and **Not now**, and a reminder notification comes one hour before the start. To turn the popups off, open the Contests screen and switch off **Event announcements**. Tracking needs a paired desktop.

## Account and Privacy

- **Settings > Account > POTACAT Cloud.** The sign-in field is *EMAIL OR CALLSIGN*. Every account shows a *Desktop sign-in:* line with your callsign.
- **Settings > Account > POTACAT Cloud > API keys.** Create and revoke POTACAT Cloud API keys. The row shows only when you are signed in to Cloud.
- **Settings > Account > Privacy & data > Share anonymous usage and crash reports.** Off stops crash reports at once. The app masks addresses, tokens and your own callsign in crash data.

## Not on the Phone Yet

As of the released 1.5.x app:

- No APRS screen. Use the desktop window or ECHOCAT Web. See [APRS](aprs.md).
- No **Send 73** for an unlogged FT8 contact.
- No Winlink Archive button, Deleted folder, Restore, Reply all, Cc or forms.
- No Bluetooth PTT button. Bluetooth MIDI paddles work.
- No switch to turn WSJT-X Mode off from the phone.
