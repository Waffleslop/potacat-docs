# Tune Links

A web page can carry a link that tunes your radio in POTACAT. Click it and POTACAT moves your radio to that frequency and mode, just as if you had clicked the spot in POTACAT's own spot table. Your browser may ask whether to open POTACAT the first time; allow it.

## Where Links Come From

- **POTACAT Cloud's on-air pages** show a **Tune** button beside a report that is live, meaning heard in the last 15 minutes, with the note *Needs POTACAT on this computer.* The button is hidden on phones and tablets. It has been there since 20 November 2026.
- Anyone can put such a link on their own page.

## The Form

`potacat://tune/<kHz>/<MODE>`

- `<kHz>` is the frequency in kilohertz, and may have decimals: `potacat://tune/14074/FT8`, `potacat://tune/14285.5/SSB`.
- `<MODE>` is optional. Without it, only the frequency changes and the radio keeps its mode: `potacat://tune/7025`.
- Upper or lower case both work for the mode.
- The short form `potacat://7025:CW` does not work. Nothing happens.

## What a Click Does

The same as clicking a spot in POTACAT:

| Mode in the link | What the radio does |
|---|---|
| FT8, FT4, FT2 | A link that points into a dial's passband, from 500 Hz below the usual dial frequency to 3 kHz above it, tunes the dial itself. `potacat://tune/14075/FT8` tunes 14.074 MHz. |
| SSB | POTACAT picks the sideband by frequency: USB from 10 MHz up, LSB below 10 MHz, and USB on 60 m. |
| CW, USB, LSB, AM, FM | As given. |
| FT8, FT4, FT2, DIGU, PKTUSB, PSK31, JS8, WSPR, JTTY | The radio's upper-sideband data mode, or plain USB when JTCAT's **Switch radio to DATA mode (PKTUSB) for FT8 / FT4** is off. |
| DIGL, PKTLSB | The radio's lower-sideband data mode. |
| RTTY | The radio's RTTY mode. |
| A mode word POTACAT does not know | The frequency changes and the mode is left alone. |

- A voice or CW link stops FT8/FT4 decoding, as a voice or CW spot click does.
- A frequency of zero, a negative one, or one above 2,000,000 kHz is refused, and nothing moves.
- A frequency outside the ham bands is tuned, for listening, and the CAT log notes it.
- During a Guest Pass a tune link is allowed, as any tune is. Whether a guest may transmit there is checked when they transmit.

## It Never Presses PTT

A tune link moves the radio and does not transmit.

> **Warning:** There is one exception. With **Auto-tune ATU on band change** ticked in **Settings > Tuning**, a link that changes band starts the radio's tuner, exactly as a spot click on another band does. Most tuners send a short carrier to tune.

## A Link Stops Automatic Transmitting First

> **New in POTACAT 1.14.7.**

If the FT8 window is transmitting on its own when a link arrives, POTACAT stops it before tuning, so nothing keeps transmitting unattended on the new frequency.

- It stops Run, Hunt, the WSPR beacon, a Spot Target waiting to call, a QSO in progress, TX left enabled, and the tune carrier. It is the same stop as the **Halt TX** button.
- Receiving carries on.
- The main window, and the FT8 window if it is open, show a notice, for example *A tune link moved your radio to 14.074 MHz. Run was stopped so nothing transmits on the new frequency.*
- When nothing was transmitting, there is no notice.
- A spot click inside POTACAT is not changed by this.

## A Link That Starts POTACAT Waits for the Radio

> **New in POTACAT 1.14.7.**

Clicking a link when POTACAT is closed starts it. POTACAT holds the link until the radio is connected and has reported its frequency, then tunes once.

- If you click another link meanwhile, only the last one counts.
- If the radio has not connected after 60 seconds, the link is dropped with the notice *Could not tune: the radio did not connect*.
- The same wait applies when POTACAT is already open but the radio has not connected yet since it started.
- Once the radio has been connected, links tune at once.
- With no radio set up, links go straight through.

## Which Computers

The POTACAT installers register `potacat://` on Windows, macOS and Linux. Windows and macOS are the ones in use. Linux is untested, and depends on the Linux package and desktop.

## The Other Two potacat:// Links

- `potacat://pass/<code>` opens a Guest Pass in POTACAT and connects to the shared radio as a guest. See [Share Your Rig](../echocat.md#share-your-rig).
- `potacat://pair?...` is a pairing link for running your shack from another POTACAT. Clicking it works as well as pasting it. See [Pairing](remote-desktop.md#pairing).
