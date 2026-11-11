# Directory

Directory is a list of things to tune to that aren't spots: nets, shortwave broadcasts, signals that are always on the air, and your own frequency chart. Open it from **More ▾ > SWL/HF Net Directory**. It needs no setting.

It has four tabs: **HF Nets**, **SWL Broadcasts**, **Landmarks** and **Channels**. Click a row to tune it. The Up and Down arrow keys step through the rows.

ECHOCAT Web has the same lists under its **Dir** tab.

## Landmarks

Signals worth dialling into at any time, each with a line saying what it is: the time stations (WWV, WWVH, CHU and RWM), the NCDXF beacons, NOAA weather, the calling frequencies and a few oddities.

- Click a row to tune it. The panel beside the list explains it: **What you'll hear**, **Why it matters** and **Try this**.
- On a beacon frequency, the panel names the beacon transmitting right now.
- The first time you open the tab it suggests WWV on 10 MHz. A tick every second means the radio, the antenna and the audio all work.
- The category filter narrows the list: Time signals, Beacons, Weather, Calling frequencies and more.
- A landmark only your SDR can hear is shown with an **SDR** tag.

## Channels

A frequency chart that is yours to edit. It starts with FRS, GMRS and its repeater pairs, MURS, the marine VHF channels with what each is for, aviation calling and guard frequencies, public-safety interop and the EMS Med channels.

- Drag to reorder, edit, delete, or add your own.
- **Import CHIRP CSV** brings in your handheld's programming file. **Export CSV** writes the chart back out.
- A starter channel you delete stays deleted. **Restore starter channels** brings them back.
- A click tunes the channel, through the SDR when your radio can't reach it.

### CB channels

From 1.14.3, Channels has a **CB (Citizens Band)** group with all 40 channels by number. Channel 9 is marked for emergencies and channel 19 for highway traffic.

### Recall the radio's own memory

From 1.14.3, a channel can carry the number of one of the radio's memories. Edit the channel and fill in **Radio memory**. A click then recalls that memory on the radio, with its offset and tone, instead of tuning the frequency. Leave it blank to tune the frequency as before. A channel with a memory number shows an **M** badge in the list, such as **M12**.

This works over Icom CI-V and over rigctld.

## Favorites

> **New in POTACAT 1.14.3.**

Star a Landmark (a NOAA weather station, say) or a Channel. Starred entries appear:

- under **Favorites** in Directory,
- in the [VFO window](vfo-window.md),
- as markers along the top of the band scope,
- in ECHOCAT Web.

Favorites belong to each operator profile.

## When the radio can't go there

When POTACAT can't move the radio to a frequency (there is no CAT link, or the frequency is outside the radio's range), a tune listens through an SDR that covers it. From 1.14.3 this also happens for a tune from ECHOCAT, and POTACAT connects a listed SDR first if needed. See [WebSDR, KiwiSDR and RTL-SDR Receive](websdr.md).
