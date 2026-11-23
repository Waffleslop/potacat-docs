# The ECHOCAT App: What It Has Today

This page describes the ECHOCAT phone app, version 1.6.0, on iPhone and Android, with its over-the-air updates through 23 November 2026. Version 1.6.0 reached the App Store on 22 November 2026 and is on Google Play. The latest POTACAT desktop on that date is 1.14.7.

If your phone is on 1.5.x, update from the store. Version 1.5.x has an older Settings layout and lacks everything marked **1.6.0** below. **Settings > Help > About** shows your version.

Most of the app is a remote view of POTACAT on your shack computer. Where a feature needs a certain POTACAT version, the line says so; on an older desktop the feature is hidden or shows nothing.

For pairing and connection paths, see [ECHOCAT](../echocat.md) and [Connectivity & Pairing](echocat-connectivity.md).

## Updates

- App updates arrive over the air for version 1.6.0. On an older store version, update from the store.
- When an update is ready, a card at the top of **Settings** reads *An update is available* and *Tap here to install it. ECHOCAT restarts in a few seconds.* While you transmit it reads *It installs when you stop transmitting.*
- **1.6.0:** when an update has downloaded after the shack connected, a card over the app reads *An update is available*, with **Install** (ECHOCAT restarts now) and **Later** (it installs at the next launch). It shows once per launch, and **Install** is greyed while you transmit.
- A new store version gets a one-time card on Spots.
- **Settings > Help > About** has **Check for updates**, and shows the version line with the update's id. Tap the line to copy it.

## Settings

In app version 1.6.0, Settings is in six groups. Nothing was removed; some options are one level deeper. Version 1.5.x has the older groups (Hardware, Operating, Account, App, Help). This guide gives the 1.6.0 path first and the 1.5.x path after it.

In 1.6.0:

- **Search settings**, at the top, finds any option. The old row names work as search words, so typing an old name still finds it.
- The callsign card under it shows your callsign, grid, radio and shack computer. Tap it to open **Operator**. Under **GRID**, **Use my phone's location** sets your grid from one location fix; the app does not follow your location in the background.
- **Station:** POTACAT Cloud, Connection, Rig, Paired desktops, Audio, Bluetooth PTT button, Idle Mode.
- **Finding stations:** Spots, Watchlist, Scan, SDR receivers.
- **Modes:** Voice macros, CW, Digital modes, SSTV, Winlink.
- **Look & feel:** Appearance, Layout.
- **Account:** Guest Pass, Redeem a pass, Privacy & data.
- **Help:** Diagnostics, Send feedback, About.

Some rows show only when they apply: Bluetooth PTT button needs a phone with Bluetooth LE, Idle Mode shows when the desktop takes it from the phone, and Winlink shows with the Mail tab.

Where the common ones went:

| In 1.5.x | In 1.6.0 |
|---|---|
| Hardware > Radio connection | **Station > Connection** |
| Hardware > CW keyer, Operating > CW | **Modes > CW** |
| Operating > JTCAT (FT8/FT4) | **Modes > Digital modes** |
| Operating > Audio levels (TX Drive, RX Level, EQ, compressor) | **Station > Audio** |
| Hardware > Audio bridge | **Station > Audio** |
| Hardware > Rig, Paired desktops | **Station** |
| Hardware > SDR Receivers | **Finding stations > SDR receivers** |
| Operating > Spots, Watchlist, Scan | **Finding stations** |
| Operating > Watchlist groups | **Finding stations > Watchlist > Watchlist groups** |
| Operating > SSTV, Winlink; Hardware > Voice macros | **Modes** |
| Operating > Idle Mode | **Station > Idle Mode** |
| Operating > Distance | **Look & feel > Appearance > Distance** |
| App > Appearance, Layout | **Look & feel** |
| Account > Manage Account | **Station > POTACAT Cloud** |
| Account > Last Sync, API keys | **Station > POTACAT Cloud > Last Sync**, **API keys** |
| Account > Shared rigs | **Account > Guest Pass > Shared rigs** |
| Help > Rate ECHOCAT | **Help > About > Rate ECHOCAT** |
| Operating as (card at the bottom) | The callsign card at the top |

**RX Boost (1.6.0).** **Settings > Station > Audio**, in the Audio levels section, has **RX Boost** with **1x**, **2x** and **3x**. It raises the phone's own playback of the receive audio and is kept on the phone.

## Appearance

**Settings > Look & feel > Appearance** (in 1.5.x, **Settings > App > Appearance**). Choose the mode first (**System**, **Light** or **Dark**), then a theme for that mode. A new install starts on System. In 1.6.0, **Distance** (miles or kilometers) is on the same screen; in 1.5.x it is **Settings > Operating > Distance**.

- Dark themes: **POTACAT Dark** (the default), **Midnight**, **Acid Burn**, **Miami Nights**. Acid Burn sets all text in a monospaced font.
- Light themes: **POTACAT Light**, **She's On Frequency**.

These are the same six themes as POTACAT desktop from 1.14.4.

**App icon (1.6.0, iPhone only).** The same screen has **App icon**, the icon on your Home Screen: **Default**, **Midnight**, **Acid Burn**, **Miami Nights**, **POTACAT Light** and **She's On Frequency**. The themed icons come with POTACAT Cloud; without it they are dimmed. The icon goes back to Default when Cloud ends.

## The Header and Your Shacks

- The connection tag reads **LAN**, **CLOUD** or **TAIL**.
- With two or more paired shacks, tap the tag. A **Shacks** sheet lists them, with *CONNECTED* on the current one and **SWITCH** on the others. This needs POTACAT 1.14.2. A Cloud-only pairing made before 9 November 2026 may need to be paired again once.
- To remove a shack, long-press its row under **MY SHACKS** and confirm.
- While on Cloud or Tailscale, the app checks for the shack's home network every 30 seconds, and at once when the app comes back to the front, and moves to LAN when it answers. It waits if you are transmitting.
- When WSJT-X Mode is on at the shack, the app shows a banner in place of *Radio offline*, and the CAT dot in the header turns amber; tap the dot to bring the banner back. In 1.6.0 the banner is titled *WSJT-X Mode* and reads *The shack is in WSJT-X Mode. WSJT-X has the radio, so tuning and transmitting from here are off. Turn it off at the shack: click CAT in POTACAT's top bar and untick WSJT-X Mode.* In 1.5.x it reads *WSJT-X Mode is on at the shack*. The phone cannot turn WSJT-X Mode off. See [WSJT-X](wsjt-x.md).
- On narrow screens the ping readout is hidden and the frequency is sized to fit, so the Settings gear stays on screen.

## FlexRadio Direct (1.6.0, iPhone Only)

An iPhone can connect to a FlexRadio with no desktop. It needs no POTACAT Cloud. It is not on Android.

- Open **Settings > Station > Connection**. The rows are **Your desktop**, **FlexRadio direct** and **Local Rig**. With no desktop paired, a card reads *HAVE A FLEXRADIO?* with **Connect to my FlexRadio**.
- Choose **Sign in with FlexRadio** (SmartLink, from anywhere; needs a FlexRadio account) or **Connect on this Wi-Fi**.
- **What works:** tuning, the band scope, receive audio on the Audio button, FT8 and FT4 send and receive, Tune, the S-meter, RF gain, the noise blanker, and band pickers that list only the radio's own bands.
- **ATU and CW.** The **ATU** button runs the radio's tuner and stops after 30 seconds or on HALT. CW macros and typed CW go out on the radio's own keyer at the speed you set. These two have not yet been tried on a radio; a report is welcome.
- **What does not work:** voice transmit, paddle CW, JS8, SSTV, Winlink and Guest Pass. Those need POTACAT on your desktop. Preamp and squelch are off.
- **Transmit timeout.** Once per radio, before the first transmit, the app asks to turn on the radio's own transmit timeout: **Set it to 3 minutes** or **Not now (receive only)**. Every program on the radio then uses that timeout. The app never changes a timeout you have already set. ECHOCAT also stops transmitting when the link drops or the app goes to the background.

## Spots and Map

- With the Long row layout, the callsign stays pinned on the left and the middle columns slide sideways together under a column header. When everything fits, nothing scrolls.
- Frequencies in MHz show with dots between the digit groups.
- The Spots map tints the states you have worked and confirmed, and Hunt has a wanted-state choice. This needs POTACAT 1.13.2.
- The map loads without the internet.
- The Log sheet from a spot has **+ Add second operator**, then **+ Add another operator**, with no limit. The button becomes **Log N QSOs**. Each operator is logged as a separate contact, and only the first one re-spots.
- **1.6.0:** the Log sheet shows an S-meter row above the RST fields while the shack is connected and sends one.
- **1.6.0:** the Log sheet and the log form have a **Pwr W** field beside the RST fields. It fills in from the radio's reported power and follows the radio until you type in it. With POTACAT 1.14.7, a power you type on the phone is kept on the phone and in POTACAT Cloud, but the desktop keeps its own value in its log.

## Big (1.6.0)

A tab labelled **Big**, after VFO, for reading at arm's length. The screen stays awake while it is open. A **Next** / **VFO** switch picks the view, and the phone remembers it.

- **Next** fills the card with one spot: source, *NEW PARK* when it is one, time, callsign, operator name, reference, location, frequency, mode and S-meter. **Previous** and **Next** step through the filtered spots and tune the radio. Opening the tab does not tune.
- **VFO** shows the frequency large, with the S-meter, minus and plus buttons that repeat while held, and **STEP** and **BAND** steppers.
- Both views end in a Log button, which opens the Log sheet filled in, and **PTT** (hold to transmit). Everything fits one screen; on a short screen the card drops the location first, then the reference.

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
- **Drive and ALC (1.6.0).** On FT8, FT4 and FT2, a strip above **TX CQ**, **Tune** and **HALT** shows while you transmit or tune. **DRIVE** is a slider with its percentage, the same transmit power control as ECHOCAT Web. **ALC** is a bar with its percentage, shown when your radio reports ALC to POTACAT. To keep the strip open, turn on **Display > TX drive and ALC**. Needs POTACAT 1.14.7. Not shown on FlexRadio direct, and not yet tried on a radio.
- **Not on the phone:** the *Not logged* notice and **Send 73** button for a contact that ended before any 73. Use ECHOCAT Web or the JTCAT window. See [When a contact is logged](jtcat.md#when-a-contact-is-logged).

**Settings > Modes > Digital modes** (in 1.5.x, **Settings > Operating > JTCAT (FT8/FT4)**) has two more:

- **Keep screen on:** **Never**, **Scanning or decoding** or **Whenever connected**. Scanning or decoding covers Scan, FT8, FT4, FT2, WSPR, PSK, JTTY and JS8. The phone sleeps as usual once it loses the shack.
- **JTTY alerts:** **Off**, **My call** (the default) or **Any message**. You get a toast in the app, or a notification when you are on another tab or in another app. On an iPhone, alerts in the background need Audio on.

**JS8** has an **Inbox** / **Activity** switch. Activity lists every decoded frame, heartbeats included. Tap a row to open its thread.

**WSPR:** the band list includes 2 m. Idle Mode offers 2 m only when the shack's radio lists 2 m, and needs POTACAT 1.14.0.

## Pan (Panadapter)

A tab labelled **Pan**, for radios that send a band scope to POTACAT. It shows a full-screen scope and waterfall, a tuning card, a swipe strip for tuning, and a PTT button (**Key** and **Stop** in CW).

- Drag to tune. Tap the tuning card for the keypad.
- A FlexRadio panadapter and the FT-710 scope need POTACAT 1.13.6. Icom scopes need 1.13.7.

On the **VFO** tab, the scope section is called **Waterfall**. It shows the radio's own scope where there is one, otherwise the receive-audio waterfall.

## APRS Tab

In app 1.6.0. A tab labelled **APRS**, after Map. It needs POTACAT 1.14.7 and shows once the desktop has sent its APRS state; until then the screen reads *Waiting for APRS from the desktop.* See [APRS](aprs.md) for what the desktop does.

- **Filter:** **2 m**, **30 m** or **Both**. 2 m is what the radio hears on 2 m plus internet stations within the distance; 30 m is what the radio hears on 30 m, at any distance.
- **Distance:** the chip beside the filter (for example *Within 50 mi*) opens **APRS settings**, with distance choices in your own unit.
- A switch changes between the map and the list. **Search callsign or name** searches the stations the phone holds.
- **Listen** / **Stop listening** starts and stops listening on the radio. If the shack is decoding FT8, a sheet asks first; **Listen** then stops FT8 and starts APRS.
- **Band** opens **Band and radio settings**, with **Band to listen on** and **Report what I hear (iGate)**.
- **Beacon** opens a sheet with **Send over the internet**. After a send it reads, for example, *Sent 11:34 · seen on APRS-IS*.
- Tap a station for its sheet: distance, last heard, whether it is moving and how it was heard.
- **Not on the phone:** a beacon on the radio (with POTACAT 1.14.7), APRS messages and your own beacon text. Nothing on the APRS tab transmits by itself. A Guest Pass sees the map, the list and the filter only.

## Radio Controls

- **Split.** Rig Controls has a **SPLIT** section with a **TX, VFO B** row, offset chips (**-1k**, **+1k**, **+5k**, **+10k**) and a TX frequency keypad. Offsets are from the receive frequency. The VFO tab shows a TX line and a SPLIT tag. Needs POTACAT 1.13.9. An IC-7300 with firmware older than 1.30 cannot set VFO B.
- **Rig presets** are on the VFO tab. When the desktop applies one, the phone shows a notice titled *Rig preset* and its name, with what changed. Needs POTACAT 1.13.0.
- **ATU.** The tune button lights only while the tuner is sweeping.
- **A radio with no CAT,** keyed by its sound card, gets the PTT button, and the *Radio offline* banner is hidden for it.
- **PTT release** ends with a 150 ms tail before the radio unkeys, so a radio that switches to DATA mode on key-down no longer clips. Safety releases are still immediate.
- A tune from Spots, Dir, Map, Pan, the VFO keypad or Act while an SSTV picture is being received asks before taking the radio.
- **XIT (1.6.0).** In CW, the CW bar at the bottom of the screen has an **XIT** chip beside the speed box. Tap it to turn XIT on or off; when on, it shows the offset, for example *+150*. Press and hold for a sheet where **−** and **+** step 10 Hz, from -999 to +999 Hz, with **Off**. POTACAT uses the offset the next time it tunes to a CW spot, not on the frequency you are already on. Needs POTACAT 1.14.7. Hidden on FlexRadio direct and Local Rig, and not yet tried on a radio.
- A MIDI keyer with no saved mapping, plugged in or on Bluetooth, keys on its own device preset. A mapping you taught the app still wins.

### Bluetooth PTT Button

In app 1.6.0, on iPhone and Android, on a phone with Bluetooth LE. A Bluetooth speaker-mic button can key the radio.

- Open **Settings > Station > Bluetooth PTT button** and tap **Pair a button**, then **Pair** beside it under *BUTTONS NEARBY*. The test on that screen lights while the button is held and does not key the radio.
- Press keys the radio and release unkeys it. It works only while the audio bridge is on and the radio is in a voice mode.
- A hold stops after 3 minutes. Fifteen seconds before, a card reads *Transmit stops in 15 seconds* with **Keep transmitting**, which adds 3 minutes. With the screen locked the warning is a vibration only.
- Losing the desktop or the button ends a hold. Going to the background does not.

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
- **1.6.0:** a row shows the power (for example *5 W*) beside the RST when the contact has one. A **QRP** toggle in the search box shows contacts at 5 W or less; contacts with no power never match.

## SSTV

- The template browser has a read-only **FROM DESKTOP** section.
- Templates are saved in stages, with **CQ**, **Reply** and **73** chips and counts. Reply templates use THEIR CALL and REPORT fields. Saving templates to the shack needs POTACAT 1.14.6.
- A 73 card on the SSTV screen opens Compose and does not transmit.
- The text editor has typeface, outline, shadow and letter spacing. Needs POTACAT 1.14.3.
- The control bar has an ATU button, hidden while sending.

See [SSTV](sstv.md).

## Mail (Winlink)

A **Mail** tab with the folders **In**, **Out**, **Sent** and **Archive**. Needs POTACAT 1.13.1. See [Winlink Email](winlink.md#from-your-phone-or-a-browser).

- Account setup is in **Settings > Modes > Winlink** (in 1.5.x, **Settings > Operating > Winlink**). With no password saved, the Mail tab opens on *Set up your Winlink account*.
- The composer queues with **Put in Outbox**. **Send / Receive** on the Mail tab is what transmits. In 1.6.0 the composer has a **Cc** field.
- The send sheet has **Send via**, **FAVORITES** (starred gateways, kept per frequency), **RADIO DIAL**, **Refresh** and **History**. Favorites and History need POTACAT 1.14.4.
- When the channel is busy, a card shows the shack's wait and has **Call anyway**, with the line *Call anyway only if you have listened and it is clear.*
- **1.6.0:** when a gateway does not answer, the card has **Try again** and **Choose gateway**. The gateway prediction counts down (*Predicting, about 12 s left*).
- The tab shows the radio's own waterfall when the radio sends a scope. In 1.6.0 the modem's channel is drawn on it as one shaded band with its name and width, for example *VARA 2300 Hz*.
- While the tab is open the radio stays on the gateway. Needs POTACAT 1.14.6.
- **A copy on the phone (1.6.0).** The phone keeps your folders and every message you have opened. Away from the shack you can read them; writing, Archive, Move and Delete wait until you reconnect. The copy never goes to POTACAT Cloud, it is erased when you remove the pairing, and a Guest Pass never keeps one.
- The message bar has **Reply**, **Mark unread** and **Delete**.
- **Not on the phone:** an Archive button, a Deleted folder, Restore, Reply all and, with POTACAT 1.14.7, Winlink forms. You can read archived mail in the Archive folder. Use ECHOCAT Web or the desktop for the rest.

## Guest Pass

Needs POTACAT 1.14.6 for the parts below; an older desktop keeps the older behaviour. See [Share Your Rig](../echocat.md#share-your-rig).

- A guest sees one banner and card saying whether they are on the air, waiting, reconnecting, or the pass is over. Only an ended pass ends the session.
- The card's buttons are **Leave**, **Use it here instead**, **Take the radio**, **Stop** and **Close**. When the owner has been idle, the guest is told *Press Take the radio to go back on the air.*
- Notifications report the changes.
- A guest can listen on the station's SDRs and stop them, nothing else.
- On the owner's side the button is **Cancel pass**.
- When you make a Guest Pass on an account with two or more shacks, you pick the shack.
- **1.6.0:** the share text is one message with the link once. The take-over dialog shows the time left, with **Not now** and **Take over**. My passes shows each pass's state from its expiry, for example *Expires 22 Nov 04:20 UTC · 3 h left* or *Ended 14 Nov 02:00 UTC*.

## Special Events

When POTACAT announces a special event, a one-time popup headed *POTACAT EVENT* appears, with a tracking choice and **Not now**, and a reminder notification comes one hour before the start. To turn the popups off, open the Contests screen and switch off **Event announcements**. Tracking needs a paired desktop.

## POTACAT Cloud, Privacy and Help

- **Settings > Station > POTACAT Cloud** (in 1.5.x, **Settings > Account > Manage Account**). In 1.6.0 the row shows your plan and the last sync, or *Not signed in*. The sign-in field is *EMAIL OR CALLSIGN*. Every account shows a *Desktop sign-in:* line with your callsign.
- **Settings > Station > POTACAT Cloud > API keys** (in 1.5.x, **Settings > Account > API keys**). Create and revoke POTACAT Cloud API keys. The row shows only when you are signed in to Cloud.
- **Trial offer (1.6.0).** Once on each phone, on your home network, when neither the shack nor the phone has POTACAT Cloud, a sheet offers a POTACAT Cloud trial, with **Start free trial** and **Not now**. Start creates the account and signs the shack and the phone in. It is not shown to a Guest Pass guest, on Local Rig or on FlexRadio direct.
- **Settings > Account > Privacy & data > Share anonymous usage and crash reports.** Off stops crash reports at once. The app masks addresses, tokens and your own callsign in crash data.
- **Settings > Help > Diagnostics.** In 1.6.0 this is one report card with **Send report**, which opens the share sheet, and **Copy**. The report always has private details masked.

## Not on the Phone Yet

As of app 1.6.0 with POTACAT 1.14.7:

- No APRS beacon on the radio, APRS messages or own beacon text. See [APRS](aprs.md).
- No **Send 73** for an unlogged FT8 contact.
- No Winlink Archive button, Deleted folder, Restore, Reply all or forms.
- No switch to turn WSJT-X Mode off from the phone.
- No FlexRadio direct on Android.
