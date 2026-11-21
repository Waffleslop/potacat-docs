# APRS

> **New in POTACAT 1.14.7.**

APRS (Automatic Packet Reporting System) is short data packets that stations send with their position, a symbol and a short comment. iGates pass what they hear on the radio to the internet, where the network is called APRS-IS. POTACAT shows APRS stations on a map from two places: the internet (APRS-IS) and your own radio.

## Open the Window

In the main window press **More ▾**, then **APRS ↗**. The **APRS** window remembers its size and place. Across the top are **Map** and **Messages**, the two views, and **APRS settings**.

## The Three Cards

### My radio

One switch turns listening on your radio on and off. Listening is receive only: nothing is transmitted.

- **Band.** When the radio has both 2 m and 30 m, a band box sits beside the switch. A radio with only HF gets 30 m. A radio with 2 m gets 2 m unless you pick 30 m.
- **Off,** the card reads *Not listening on my radio* and says where the radio goes back to when you stop.
- **On,** it reads *Tuning my radio to APRS*, then *Listening on my radio* with the band, frequency and speed (for example *2 m · 144.390 MHz · 1200 baud*) and an S-meter.
- When you switch it off, POTACAT puts the radio back where it was.
- The switch cannot be moved while a radio beacon has the radio.

**Frequencies.** The 2 m frequency is chosen from the grid square in Settings:

| Where | 2 m frequency |
|---|---|
| US and Canada | 144.390 MHz |
| IARU Region 1 (Europe, Africa, the Middle East, the former USSR, Mongolia) | 144.800 MHz |
| Australia | 145.175 MHz |
| New Zealand | 144.575 MHz |

Other countries have no 2 m entry yet, and the card says *POTACAT has no APRS frequency for your grid square yet.* On 30 m the frequency is 10.1476 MHz USB everywhere. The mode is FM on 2 m and the radio's upper-sideband data mode on 30 m, or plain USB if JTCAT's **Switch radio to DATA mode (PKTUSB) for FT8 / FT4** is off.

**When listening cannot start,** the card says why in one sentence:

- *Connect your radio to listen to APRS.*
- *Your radio has neither 2 m nor 30 m.*
- *POTACAT has no APRS frequency for your grid square yet.*
- *Dire Wolf is not available on this computer.*
- *FT8 is decoding. Stop it to listen to APRS.*
- *A Winlink session has the modem.*
- *Listening runs on the computer the radio is connected to.* This shows on a POTACAT that drives a remote shack.
- *The radio did not accept* the frequency.

On 30 m, if Settings has a digital filter narrower than 1000 Hz, the card warns that APRS on 30 m needs 1500 to 1900 Hz to pass. POTACAT does not change the filter for listening.

### APRS-IS

One switch turns on the internet feed of stations near your grid square. It is read-only. The card reads *Connected to APRS-IS* with the server and packets a minute, *Connecting to APRS-IS* or *Not connected to APRS-IS*. With no grid square in Settings it says *Set your grid square in Settings to see the stations near you.*

The second line is the iGate, for example *iGate off* or *iGate on: 3 packets from my radio sent up*. **iGate settings** opens APRS settings.

### Heard by my radio

How many stations your own radio has decoded since the window opened, and the last one, for example *Last: W1ABC-9, 2 min ago, 12 mi*.

## Listening Starts When You Open the Window

Opening the APRS window turns on listening on your radio, once. It tunes the radio and never transmits, and it changes nothing about either beacon.

It does not start when:

- listening is already on, from the switch, Idle Mode or an ECHOCAT device
- anything is transmitting, or a radio beacon is on its way
- an FT8 contact is in progress, or JTCAT, Winlink or Mercury has the radio
- a Guest Pass is in use on this station
- any of the reasons listed under [My radio](#my-radio) applies

If you switch listening off, it stays off until you close the window and open it again.

## Listening Pauses When the Radio Moves

If the radio leaves the APRS frequency or its mode while listening (a spot click, a tune from a phone, the VFO knob, another window), listening pauses and lets go of the radio. The card reads *Paused: your radio moved* and says where the radio is now. The radio stays where it was put. Switch listening on again to tune back to APRS.

Small differences, such as the radio's own rounding, do not count as a move.

## The Map

- Each station is a pin with an icon for its kind: house, car, boat, aircraft, hiker, weather station, digipeater, iGate and others. Cars, boats and aircraft point the way they are going.
- Zoomed out, nearby stations gather into a circle with a count. Click it to zoom in.
- Zoomed in, each pin has a callsign label. Click the pin or its label to select the station. Its details show under the list: position, distance and direction from you, speed, altitude, weather, comment, when and how it was heard, the raw packet, and a **QRZ** button that opens QRZ.com in your browser.
- Stations your own radio decoded have a green ring.
- Your own position is marked with your callsign. When your beacon is less exact than your home position, the label says what others see, for example *W1ABC (beacon: about 1 mile)*.
- **Heard by my radio** / **Everyone** switches the map between the stations your radio heard and every station. The list always shows everyone, your radio's stations first.
- The **Home** button under the zoom buttons goes back to your home area.
- The first time, the map opens on your home area. After that it opens where you left it.

## The Stations List

The header counts the stations, for example *3 by my radio, 138 on the internet*.

- **Search** by call sign or comment.
- **Within:** how far from your grid square APRS-IS sends stations: 25, 50, 100, 250 or 500 mi, or 25, 50, 100, 250, 500 or 800 km, in your Settings distance unit. Picking one also centres the map on your home area.
- **Show the last:** how long a station stays in the list and on the map after it was last heard: 15 min, 30 min, 1 hour, 3 hours or 6 hours. It starts at 1 hour. Older stations are drawn fainter.
- **Clear** empties the list, the map and the Heard by my radio count straight away, without asking. APRS-IS and listening keep running, and new stations fill the list again.

## Beacons

A beacon is one packet with your position, symbol and comment. The Beacon panel's header says who beacons go out as, for example *Beacons as W1ABC-7 (internet W1ABC-10)*. **Change** opens APRS settings.

### Power

**Power**, with **−** and **+**, is the radio's own transmit power as the radio reads it back. The radio beacon goes out at this power and never changes it. A radio whose power is not available over CAT shows *not over CAT*; set it on the radio.

5 W is fine to start. APRS on 2 m commonly runs 5 to 50 W. On 30 m, a few watts to 50 W can reach an iGate, depending on conditions.

### Beacon on the radio

The button reads **Beacon on 2 m** or **Beacon on 30 m**. One click sends one packet over your radio, on the band you are listening on.

> **Warning:** There is no confirmation box and no timer. One click, one packet, on the air.

Under the button is the frequency and power, for example *144.390 MHz at 5 W, one click*. When it cannot send, the button is greyed and the line under it says why, for example:

- *Turn on Listen on my radio first. The beacon goes out on the frequency it listens on.*
- *Wait until the radio is listening.*
- *Set your callsign in Settings first.*
- *The SWR guard has tripped. Check the antenna first.*
- *JTCAT has the radio.* or *A Winlink session has the radio.*

POTACAT waits for a clear channel before keying. While it transmits:

- A red banner says *On the air: APRS beacon on* the band, with a running time and **Stop transmitting**.
- **Power out** and **SWR** bars show live readings.
- The My radio card reads *Transmitting on* the band and *Listening resumes when it ends*.

A beacon takes about 1.5 s on 2 m and about 3 s on 30 m. POTACAT unkeys on its own if one runs much longer, and closing the window stops it at once. Afterwards a line gives the last one, for example *Last radio beacon 2 min ago · 2.1 s · 4.1 W out · SWR 1.3*. A beacon counts as sent only when the radio reports that it transmitted.

The path is WIDE1-1,WIDE2-1 on 2 m and WIDE1-1 on 30 m.

**On 30 m,** the APRS signal sits just below the top of the band, 10.150 MHz.

- On a FlexRadio, POTACAT narrows the transmit filter to 1400-2000 Hz for the beacon and puts your own filter back afterwards.
- On other radios POTACAT cannot set the transmit filter. A radio whose transmit filter is wider than about 2400 Hz may refuse to transmit there, so set a narrower one on the radio.

### Beacon on the internet

One click sends your position to APRS-IS over the internet, as your callsign with -10. Nothing goes out on the air. The line under it says *Last beacon:* and the time, *Not sent yet*, or why it cannot send.

### Internet timer

**Internet timer** is Off, 10 min, 20 min or 30 min. It starts at Off. It sends your position to APRS-IS over the internet at that interval while the window is open. Nothing goes out on your radio.

- While it is set, a banner says so, with the time of the next beacon and **Stop the timer**.
- Picking a time or opening the window sends nothing at once. The first beacon is one interval later.
- The timer stops when the window closes.

## APRS Settings

Press **APRS settings** at the top right. **Done** closes it.

### iGate

**Report what I hear to APRS-IS (iGate)** is off to start. With it on, each packet your radio hears goes to APRS-IS under your callsign with -10, so it shows on APRS maps as heard by you. It applies whenever POTACAT listens to APRS on your radio, in this window or in Idle Mode. Nothing from the internet is ever sent on the air.

During a Guest Pass the iGate sends nothing and says *iGate paused: a guest has the radio*.

### My APRS SSID

The call sign ending for the radio beacon: **As my Settings callsign**, which is the starting choice, or None and -1 to -15, each with its usual meaning (for example *-7 handheld radio*, *-9 primary mobile*). Your Settings callsign is not changed. The internet beacon and the iGate always use -10.

### Position

Four choices, each with a line saying what others see:

| Choice | What it shows |
|---|---|
| **Grid square, 4 characters** | The middle of an area about 110 km tall and up to 220 km wide. |
| **Grid square, 6 characters** | About 4.6 km by up to 9 km. Greyed when your Settings grid has only 4 characters. |
| **Near my home (about 1 mile)** (*about 2 km* with km units) | Within about a mile of home, never at your door. |
| **Exact position** | The point you pick on the map, to about 20 m. Without one, the middle of your grid square. |

Until you pick one, POTACAT chooses:

- **Near my home** when your home position is better than a 4-character grid: a point picked on the map, a radio GPS fix, or a 6-character grid square.
- **Grid square, 4 characters** when the only position is a 4-character grid square.

A choice you make is kept.

**Pick on map** sets your point: click the map where you are. **Cancel** or Esc stops. **Use my grid** goes back to the grid square. With a FlexRadio that reports a GPS, two more choices appear: **From Settings or the map** and **From my radio's GPS**, which is usable once the GPS has a fix.

### Symbol and comment

- **Symbol on the map:** House, Portable, Car, Hiker or Boat. It starts as House.
- **Comment:** sent with every beacon, up to 43 characters. It starts as `POTACAT`.
- **Add my activation to the beacon comment** is off to start. While an activation runs, the comment starts with the park, frequency and mode, for example `POTA US-1234 14.062 CW`, on both beacons.

## Messages

Press **Messages** at the top. A number beside it counts unread messages.

> **Note:** Messages go out over the internet only (APRS-IS), never on the radio.

- Conversations are on the left, with a search box and **New**.
- Write in **To** and the message box, up to 67 characters, then press **Send**.
- POTACAT retries at 30 s, 1, 2 and 5 min until the other station acknowledges.
- Each message shows its state: *Waiting for APRS-IS*, *Sending, try 2 of 5*, *Delivered (ack)*, *Rejected (rej)*, *Stopped* or *No reply after 5 tries*.
- **Stop** stops a message that is going out. **Send again** resends one that failed. **Delete conversation** removes one.

### Templates

**Templates** fill **To** and the message. Nothing sends until you press **Send**.

- **Groups and nets:** **Group CQ** (ANSRVR), **Join APRSThursday** and **Leave APRSThursday**.
- **Gateways:** **Email** (EMAIL-2: the address first, then the text) and **Weather report** (WXBOT: a US city as City,ST or a 5-digit zip code).
- **My templates:** **Save current message as a template**. Fields such as `<PARK>`, `<FREQ>`, `<MODE>` and `<CALL>` fill in each time. Any other `<FIELD>` must be replaced before **Send** works.

## In a Browser (ECHOCAT Web)

ECHOCAT Web has an **APRS** tab: the station list and map, **Listen on my radio** with the band, **Report what I hear (iGate)** and **Beacon now (internet)**.

- It cannot send messages and cannot beacon on the radio.
- The internet timer is in the desktop window only.
- A guest on a Guest Pass may watch and listen, but not beacon or change the iGate, because beacons and the iGate go out under the owner's callsign.
- The APRS feed keeps running for a connected device with the desktop window closed.

## Idle Mode

In **Settings > Station**, **Idle Mode** has an **APRS** choice: the radio listens on the APRS frequency, 2 m if it has 2 m, else 30 m. It is receive only, and it runs with the APRS window closed. The iGate setting applies to it.

## Computers and Limits

- Listening and the radio beacon use Dire Wolf, which is in POTACAT's Windows, macOS and Linux installers. The APRS-IS map, the internet beacon and messages need no Dire Wolf.
- 30 m APRS is 300 baud; 2 m is 1200 baud. On 30 m POTACAT decodes and sends the ordinary 300-baud signal only. Robust Packet (RPR) signals are not decoded.
- APRS on the radio runs on the computer the radio is connected to, not on a POTACAT that [drives a remote shack](remote-desktop.md).

## What Has Been Tried on the Air

As of 1.14.7:

- **30 m on a FlexRadio:** listening, the iGate passing a packet to APRS-IS, and one radio beacon have each been confirmed, on one radio. The 30 m beacon has not been tried on any other radio.
- **2 m:** neither listening nor the radio beacon has been confirmed on the air yet.
- **Messages:** not yet tried on the air.
- **Mac and Linux:** listening has been tried on Windows only.

If you try any of these, please send a report from [Report a Bug](../community--support.md#report-a-bug).
