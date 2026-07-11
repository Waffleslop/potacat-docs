# Frequently Asked Questions

The questions that come up most often, with settled answers. If you don't find yours here, try the search box at the top of the page — and if the docs still let you down, ask in the Discord.

## Apps and pricing

#### What's the difference between POTACAT, ECHOCAT, JTCAT, and CWCAT?

They're a family, and most of them live inside one app:

- **POTACAT** is the desktop app — a free, open-source hunter/activator tool for POTA, SOTA, and DX. It connects to your radio via CAT, shows live spots, one-click tunes, and logs your contacts.
- **ECHOCAT** is the remote control for POTACAT. It's a server built into the desktop app — there's nothing separate to install on the shack computer. You connect from a phone or tablet, either in a browser (ECHOCAT Web) or with the native iOS/Android apps. See [ECHOCAT Connectivity](nested/echocat-connectivity.md).
- **JTCAT** is the FT8/FT4 engine built into POTACAT. It decodes and transmits digital modes natively — you don't need WSJT-X — and it works remotely through ECHOCAT too.
- **CWCAT** is a separate app: a CW skimmer for FlexRadio.

#### Is there a phone app?

Yes. **ECHOCAT** has native apps on the Apple App Store and Google Play for a one-time $9.99 purchase — a single lifetime fee that includes all updates. If you'd rather not pay, **ECHOCAT Web** (the browser version) stays free.

Either way, the app is a remote control: you still run POTACAT on a Windows, Mac, or Linux computer connected to the radio, and the phone connects to it. For the ways to connect — same Wi-Fi, Tailscale, or POTACAT Cloud — see [ECHOCAT Connectivity](nested/echocat-connectivity.md).

#### Is POTACAT really free? What costs money?

POTACAT desktop and ECHOCAT Web are free and open source, and always will be. Two things are paid:

- **ECHOCAT mobile apps** (iOS/Android): $9.99, one time.
- **POTACAT Cloud**: an optional subscription at $5/month or $50/year, with a free trial when you activate it inside POTACAT. Cloud adds conveniences like cloud log backup and multi-device logging, parks-worked sync, a tunnel that connects your phone to your shack without a VPN, and rig sharing with other operators.

#### Which platforms does the desktop app support?

Windows, macOS, and Linux (including arm64), with installers for all three at [potacat.com](https://potacat.com). Users have also run it successfully on a Raspberry Pi 5. Chromebooks are not a supported platform.

## Features you might have missed

#### Can I look up my previous QSOs with a callsign?

Yes. Press `Ctrl+L` and type the callsign — the logger shows your past QSOs with that station, whether or not they're currently spotted. The pop-out logger has a Past QSOs panel that does the same thing.

#### Do I need to respot an activator after I work them?

No. When you log a POTA QSO with `Ctrl+L`, the activator is respotted automatically (you can turn this off in the log dialog). `Ctrl+R` respots the selected spot without logging anything.

#### How do I get operator names to show on spots?

Enter your QRZ credentials at **Settings > Station > QRZ Name Lookup**. A regular QRZ account is all you need — name lookup does not require a paid QRZ subscription.

#### Can I sort the spot table by more than one column?

Yes — click a column header to sort, then `Shift`+click a second column for a secondary sort.

#### The text is too small (or too big).

Use `Ctrl` `+` to zoom in, `Ctrl` `-` to zoom out, and `Ctrl` `0` to reset.

#### Where's the list of keyboard shortcuts?

Press `F1` for the full hotkey list, or see [Keyboard Shortcuts](keyboard-shortcuts.md).

#### Can I send my own CAT commands to the radio?

Yes. Click the **Rig** button at the top of the Table view and open the **Custom** tab to create your own CAT command buttons — notch filter, split, anything your radio's protocol supports. The buttons you define also appear in ECHOCAT, so they work from your phone too. If CAT control itself is misbehaving, see [CAT Control Issues](nested/cat-control-issues.md).

#### Can I hide a spot I don't want to see?

Right-click it. You can hide the spot for 1 hour, 2 hours, 1 UTC day, or forever. Hiding applies to that callsign and frequency — not to every spot from that call — and there's a hidden-spots list where you can review and undo your choices.

#### Can I watch for a callsign only on certain bands or modes?

Yes. Watchlist entries accept a `CALLSIGN:BAND:MODE` syntax: `W1AW` matches everywhere, `K4SWL:20m` only on 20 meters, `KI6NAZ:CW` only on CW, and `W1AW:40m:SSB` only on 40 meter SSB. See [Watchlist](nested/watchlist.md).

#### How do I log a multi-operator activation, or a station at more than one park?

Commas. Enter multiple callsigns comma-separated in the call field to get one log entry per operator (pass-the-mic style), and enter multiple park references comma-separated in the reference field for n-fer contacts. See [Multi-Park Activations](nested/multi-park-activations.md).

#### Is there a way to test activating without a real park?

Yes — use the `K-TEST` park reference, a practice park for testing your activation setup. When you're done, QRT your spot on the POTA spot page so hunters don't chase it.

## How POTACAT behaves (and why)

#### What do the checkmarks next to callsigns mean?

A green ✅ means the station is in your log — you've worked them before at some point. A grey checkmark means you've already worked them on the current UTC day on that band, which is why the spot is muted. See [Hunter Mode](hunter-mode.md) for the full spot-table legend.

#### What does the yellow star mean?

That callsign is on your [watchlist](nested/watchlist.md).

#### I skipped a station and it came back after a restart. Why?

That's how Skip works: it's per-frequency, kept in memory only, and resets when the app restarts. It's designed for Scan mode — it also won't follow an activator who moves to a new frequency. If you want a spot gone for longer, use right-click hide instead.

#### When does a worked activator show up again?

A worked station stays hidden until the next UTC day, or sooner if the activator moves to a new park.

#### Why don't I have a Log button?

Logging is behind a setting. Open Settings, search for "log", and check **Enable QSO Logging** — the Log button and the Logbook appear once it's on.

#### Can I change where my log file is stored?

You can, but be careful: changing the ADIF log path starts a **new, empty log** at the new location. Your old file isn't deleted — it stays where it was — but POTACAT won't move it for you, and new QSOs land in the new file.

#### How does POTACAT know which parks I've already hunted?

From your POTA account: download your hunted-parks CSV from pota.app (under My Stats) and import it in Settings. That's what powers the NEW-park badges and the Hide Worked Parks filter. See [Hide Worked Parks](nested/hide-worked-parks.md) and [Parks Worked](nested/parks-worked.md).

#### I tapped an FT8 callsign and nothing transmitted until the next cycle. Is that a bug?

No — it's timing physics. An FT8 transmission needs about 12.5 seconds of the 15-second window, so there's roughly a 2-second grace window at the start of each cycle. Tap within it and POTACAT transmits immediately; miss it and you wait for the next cycle, exactly as WSJT-X would.

#### Why don't JTCAT's dB numbers match WSJT-X?

They aren't SNR. JTCAT's per-decode figures are its own decoder confidence scores, not calibrated signal-to-noise readings, so they won't line up with WSJT-X's dB values.

## Features that were declined (and why)

#### Will POTACAT add leaderboards, profiles, or social features?

No — POTACAT is staying in its lane as a hunting and activating tool, not a social platform. Related privacy note: your QSO logs are never exposed to anyone; cloud-stored logs are only reachable through widgets you choose to embed yourself.

#### Will POTACAT support WinLink or VARA?

There are no plans for either. WinLink would be difficult to integrate, and VARA's licensing stands in the way.

#### Can the mobile app do FT8 directly to a radio (via a digirig) without a computer?

No, and it's not on the roadmap — other apps already serve that use case well. ECHOCAT mobile does run FT8, but through your POTACAT desktop.

#### Can I run POTACAT headless on a Raspberry Pi and use it from a browser?

No. The desktop app depends on things a web app can't do — serial ports, TCP connections, subprocesses, file I/O — so a browser-only mode isn't feasible. Run the full desktop app on the Pi or shack computer and connect remotely with [ECHOCAT](echocat.md) instead.

#### Why is there no "delete all" button in the logbook?

It's deliberate, to protect you from wiping a log by accident. The log is a plain ADIF file (its location is shown in Settings), so if you truly want a fresh start, rename the file or clear its contents outside POTACAT.

#### Does POTACAT upload to LoTW?

Not yet — LoTW integration is in progress but hasn't shipped. In the meantime, you can export an ADIF from the logbook (with filters, if you like) and upload it yourself.
