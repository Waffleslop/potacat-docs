# ECHOCAT — Remote Phone Control

ECHOCAT turns your phone or tablet into a wireless remote for your POTACAT-connected radio. Tune spots, transmit, stream audio, send CW, log QSOs, and even run POTA activations — all over a secure connection.

ECHOCAT comes in two flavors:

- **ECHOCAT for iOS and Android** — native apps, available on the App Store and Google Play for a one-time `$9.99` purchase. The apps add features a browser can't do: keep listening with the screen locked, QR-code pairing, automatic switching between connection paths, and Bluetooth accessories like BLE PTT buttons.
- **ECHOCAT Web** — free, built into POTACAT, and runs in any modern mobile browser. Nothing to install.

Both work at the same time — pairing the app doesn't disable browser access.

> **Using a laptop or a second PC?** See [Run Your Shack from Another POTACAT](nested/remote-desktop.md). Running the shack computer with no monitor? See [Running Headless](nested/headless.md) (draft).

> **Note:** For radio control, the app is a remote for POTACAT Desktop — the desktop does the heavy lifting. When something misbehaves while connected to your shack, **update POTACAT Desktop first**; most of those problems are fixed there. The app's **ACT** tab also logs activations on its own; see [Activating without a desktop](#activating-without-a-desktop).

## What You Need

- **POTACAT** running on your shack PC, connected to your radio
- **A phone or tablet** with the ECHOCAT app — or a modern browser (Safari on iOS, Chrome on Android) for ECHOCAT Web
- **A connection path** between the two: your home Wi-Fi, **Tailscale**, or the **POTACAT Cloud** tunnel (see [Connection Paths](#connection-paths))

## Quick Start

### 1. Find Your ECHOCAT Address

ECHOCAT is on from install, so there is nothing to switch on. Who can reach it is set by **Access** in **Settings > ECHOCAT**: **Local network and Cloud** (the default), **Cloud only** or **Off**. See [Who can reach this computer](#who-can-reach-this-computer).

The address is on the **ECHOCAT** card, at the top of **Settings > ECHOCAT** and on **Settings > Summary**, under **Open in a browser**. Each address has a **Copy** button:

- **On your WiFi (home)**: an address such as `https://192.168.1.50:7300`. With no Tailscale and no Cloud it is the only address and has no label.
- **Away from home (Tailscale)**: shown when Tailscale is present.
- **Anywhere (POTACAT Cloud)**: shown when the Cloud Tunnel has an address. It also has an **Open** button.

The address must start with `https://`. Accept the browser's warning the first time.

If you have Tailscale installed, use the address in the **Away from home (Tailscale)** row for remote access. See [Connection Paths](#connection-paths).

You can also configure ECHOCAT from **Settings > ECHOCAT**, where you can change the port (default 7300), set a password (see [Password-protect your rig](#password-protect-your-rig)), set the PTT safety timeout, and select audio devices.

### 2. Pair the App (iOS/Android)

Pairing links the app to your desktop with a QR code — no typing IP addresses.

1. In POTACAT, open **Settings > ECHOCAT** (or **Summary**). On the **ECHOCAT** card, click **Pair my device…**. A dialog opens with a QR code and a link you can copy.
2. In the ECHOCAT app, scan the QR code — or scan it with your phone's camera app and open the link.

Pairing by QR code or link needs no approval on the desktop. The code works once.

**Tap to pair.** On the same network, the app can also discover your desktop automatically. Tap the discovered rig, and an Approve/Deny window opens on the desktop: click **Approve**. This is the setting **Allow tap-to-pair from the local network** in **Settings > ECHOCAT**, on by default.

Tap-to-pair works only from your home network or your tailnet. While the station is reachable through the POTACAT Cloud Tunnel, a tap-to-pair from anywhere else is refused, and the phone is told to scan the pairing QR instead.

> **Tip:** If the in-app scanner won't cooperate, generate the pairing URL on the desktop and open it directly in your phone's browser. For anything else that goes wrong, see the [Connectivity & Pairing guide](nested/echocat-connectivity.md).

Once paired, the app shows which path it's using — **LAN**, **TAIL**, or **CLOUD** — with the current latency in milliseconds at the top of the screen.

### 3. Or Open ECHOCAT Web in a Browser

No app? Use the free browser interface:

1. Open your phone's browser and navigate to the URL shown in POTACAT
2. You'll see a certificate warning (ECHOCAT uses a self-signed TLS certificate on the LAN) — tap **Advanced** > **Proceed** to accept it
3. If you have set a password, enter it and tap **Connect**

That's it — you're connected. You'll see the spot list, a frequency display, and the mode badge at the top.

### 4. Select Audio Devices

In **Settings > Radio** (on the rig's configuration), set the **ECHOCAT Audio Input** and **ECHOCAT Audio Output** devices. These control which sound devices carry RX audio from the radio to your phone and TX audio from your phone to the radio.

- **Audio Input**: The device that receives audio from your radio (e.g., a virtual audio cable output, or your radio's USB audio device)
- **Audio Output**: The device that sends audio to your radio's TX input

> **Tip:** You can also change audio devices from the Quick Settings panel without opening the full Settings dialog.

## Using ECHOCAT

### Tuning

Tap any spot in the list to tune your radio to that frequency and mode. The status bar at the top shows the current frequency and mode.

To tune manually, tap the **frequency display** to open the dial pad. Enter a frequency in MHz (e.g., `14.060`) and tap a step size to nudge the frequency up or down.

### Transmitting (PTT)

Tap and **hold** the red **PTT** button at the bottom of the screen to transmit. Release to return to receive. A safety timer (default 3 minutes) automatically drops PTT if you forget to release it.

The **STOP** button is an emergency kill switch that immediately drops PTT and halts any CW or digital transmission.

From 1.14.2, ECHOCAT Web always shows its **HALT** button. Before, it was hidden in CW and RTTY and whenever the radio's mode had not arrived.

**Wired earbuds (iPhone app):** a press of the earbud button keys PTT at once. Just after the audio route changes, such as when you plug the earbuds in, there's a short wait of about 1.5 seconds first. If a long press opens Siri, turn off **Press and Hold for Siri** in the iPhone's Settings.

### Audio

Tap the **Audio** button to start streaming. Your phone will ask for microphone permission — this is needed for TX audio.

- **RX audio** streams from your radio to your phone speaker/earpiece
- **TX audio** streams from your phone microphone to the radio when PTT is held
- Tap **Vol** to cycle through gain levels (1x, 2x, 3x) if RX audio is too quiet

> **iOS note:** In ECHOCAT Web, keep the browser in the foreground or use the Audio button to maintain the connection — iOS aggressively suspends background WebSocket connections. The native app doesn't have this problem: it keeps streaming with the screen locked.

### Scanning

Tap the **Scan** button in the status bar to auto-tune through your filtered spot list. The radio dwells on each spot for a configurable time (default 7 seconds, adjustable in the settings overlay). Tap Scan again or tap any spot to stop.

### Filters

Tap the **gear icon** on the phone to open the settings overlay where you can filter by:

- **Bands** (160m through 6m)
- **Modes** (SSB, CW, FT8, FM, etc.)
- **Regions** (NA, EU, AS, etc.)
- **Spot sources** (POTA, SOTA, WWFF, LLOTA, DX Cluster)
- **Max age** — hide spots older than a set time
- **New parks only** — show only parks you haven't worked
- **Hide worked** — hide callsigns you've already logged

### Radio Controls

Tap the **rig controls** button to reveal additional controls:

- **Filter width** — step the IF bandwidth narrower or wider
- **NB** — toggle the noise blanker
- **ATU** — toggle the antenna tuner (if your radio supports CAT-controlled ATU)
- **VFO A/B** — switch VFOs or swap A⇄B
- **RF Gain** slider (0–100%)
- **TX Power** slider (0–100%)

In the native app, these rig controls (including custom CAT commands) live behind the **CAT** button at the top of the screen — easy to miss if you're looking for a settings menu.

### Remote Rig Power On/Off

If your radio supports power control over CAT, you can power it on and off from your phone. In the app, the power controls are in the **VFO** tab.

From 1.14.7, **Power Off** is shown for a radio on a direct serial port or a Yaesu SCU-LAN10 and hidden for other connections, unless you choose otherwise. See [Power Off](nested/my-rigs.md#power-off).

> **Tip:** On Icom rigs, if power-*off* works but power-*on* doesn't, set the radio's **CI-V Baud Rate** to `AUTO` — CAT power-on requires a wake-up preamble that's sensitive to the baud setting.

To go fully remote, the **POTACAT Launcher** — a small companion daemon on port `7301` — lets the app start or restart POTACAT Desktop itself. It runs in the system tray and requires the installed POTACAT (not a source build).

### Rotor Control

If you have PSTRotator configured in POTACAT, a rotor toggle appears in the radio controls section. When enabled, tuning a spot automatically sends the bearing to your rotator.

## CW from Your Phone

ECHOCAT includes a full CW keyer that lets you send CW from your phone's touchscreen or a Bluetooth MIDI paddle.

### Enable CW

1. In POTACAT on the desktop, open **Settings > ECHOCAT** and, under **Remote CW Keyer**, tick **Enable Remote CW Keyer**. (**Enable CW Keyer**, under **Settings > Station**, is a different setting: the desktop's own keyer.)
2. On your phone, the CW panel appears when you're in CW mode

### CW Panel Controls

- **WPM** — adjust sending speed (5–50 WPM)
- **Keyer mode** — Iambic B, Iambic A, or Straight Key
- **Sidetone** — adjustable frequency (400–900 Hz) and volume
- **Macro buttons** — programmable CW messages, up to 25. Customize the labels and text in POTACAT's desktop settings.
- **Free text field** — type any text and send it as CW

### CW Keying Methods

ECHOCAT supports three keying methods that can work simultaneously:

1. **Text macros (KY command)** — Tap a macro button and the radio's internal keyer sends the text. Best for programmed messages with clean keying. Requires radio firmware support (QMX firmware 1\_00\_021+).

2. **Paddle CW (TX/RX keying)** — Touch the on-screen paddle or use a Bluetooth MIDI paddle. Your phone sends paddle contact events over WebSocket, POTACAT's iambic keyer generates the timing, and TX/RX commands key the radio. Preserves your sending rhythm.

3. **Hardware DTR keying** — A dedicated USB-to-serial adapter wired to your radio's key jack. Best for absolute timing precision. See the [Remote CW Setup Guide](/remote-cw-setup) for wiring details.

> **Sidetone:** For paddle CW and DTR keying, your phone generates local sidetone via its speaker — the radio's sidetone is not used since TX/RX keying bypasses the radio's internal keyer. For CW macros, the phone's sidetone plays the same words the radio sends, with your name and other macro fields filled in, at even timing. After a macro, receive audio comes back after a short tail sized to the connection: about 0.25 s on your home network, under 0.5 s over Cloud.

## FT8 / Digital Modes (JTCAT)

ECHOCAT integrates with POTACAT's JTCAT feature for remote FT8/FT4 operation.

Tap the **FT8** tab on your phone to access:

- **Band selection** (80m–6m) with one-tap band changes
- **Mode selector** (FT8, FT4, FT2)
- **Decode log** — live scrolling list of decoded stations
- **TX controls** — enable TX, call CQ, reply to stations
- **Waterfall** — live spectrum display streamed from the desktop
- **Auto QSO sequencing** — JTCAT handles the exchange sequence; you just pick who to call

**Hunt filters** (POTACAT 1.14.0): ECHOCAT Web has the same **Filters** sheet and the same status line under Hunt as the desktop FT8 window. See [Hunt filters](nested/jtcat.md#hunt-filters). ECHOCAT Web shows the saved Custom list even with Hunt off. A Guest Pass gets no Filters button. The phone app gets the Filters sheet and status line with its next update; there, you long-press a decode for **Never answer**.

## Activator Mode

ECHOCAT supports running full POTA/SOTA activations from your phone.

### Start an Activation

1. Tap the **Activate** tab
2. Select your activation type (POTA, SOTA, or Other)
3. Enter your park/summit reference (autocomplete helps you find it)
4. Tap **Start Activation**

### Logging QSOs

During an activation, tap the **Log** button next to any spot, or use the quick-log form:

- Enter callsign, RST sent/received, and optional notes
- QSOs are numbered and timestamped automatically
- A contact switched to **General** never carries the previous park. Before this fix, such a contact could be logged with the last park and count as a false park-to-park. Contacts already logged that way need the park removed by hand, and re-uploading if they were sent to POTA
- Your contact list shows at the bottom of the activation view

### Re-spotting

When you log a QSO during an activation, ECHOCAT can automatically re-spot you on POTA/SOTA/WWFF. Configure your re-spot comment template in POTACAT's desktop settings (e.g., `{rst} in {QTH} 73 {mycallsign} via POTACAT`).

### Export

Tap **Export ADIF** to generate an ADIF file of your activation contacts. Past activations are saved and viewable with individual map views showing your QSO locations.

### Activating without a desktop

The mobile app's **ACT** tab doesn't need POTACAT Desktop. Out in the field with no shack connection, it switches to a local session ("Local session — QSOs save on this phone and sync to the cloud").

**Works on the phone alone:**

- Starting an activation and logging QSOs
- Finding parks near you with the phone's GPS, offline
- Spotting yourself on POTA over mobile data
- Viewing and exporting the logbook

**Needs something else:**

- **Getting the QSOs to your desktop and other devices** goes through POTACAT Cloud sync, which is the paid Cloud plan. Without it, export the ADIF from the phone.
- **The automatic re-spot when you log a QSO** needs the desktop.
- **Logging for another operator** ("Log as") needs the desktop.

## Connection Paths

There are three ways for your phone to reach POTACAT. The app checks all of them at connect time and uses the fastest — walk into the house mid-QSO and it hands off from Cloud or Tailscale to LAN automatically. The indicator at the top of the app shows the active path (**LAN**, **TAIL**, or **CLOUD**) and the latency.

| Path | Best for | What you need |
|------|----------|---------------|
| **Same LAN** | Operating at home | Phone and PC on the same network — nothing else |
| **Tailscale** | Remote access, free forever | Tailscale on both devices, plus two admin settings |
| **POTACAT Cloud** | The "easy button" for remote access; required for rig sharing | A POTACAT Cloud account — no Tailscale, no port forwarding |

> **Tip:** Stuck at any point? The [ECHOCAT Connectivity & Pairing guide](nested/echocat-connectivity.md) walks through each path in plain English, including the two Tailscale settings that cause most failures.

### Same Network (LAN)

On your home Wi-Fi, your phone reaches POTACAT directly at its LAN IP address. No special setup needed beyond enabling ECHOCAT.

### Tailscale

Tailscale is a free VPN that connects your phone and shack PC wherever they are — and it will keep working as a supported path indefinitely:

1. Install **Tailscale** (free) on both your shack PC and your phone, signed in to the same account
2. In the Tailscale admin console at `login.tailscale.com/admin/dns`, enable **MagicDNS** and **HTTPS Certificates** — pairing fails without both, and the iPhone app can't connect over Tailscale without them
   - **Linux only:** run `sudo tailscale set --operator=$USER` once on the shack PC, then restart POTACAT and re-pair once at home. Without it, POTACAT can't get the Tailscale certificate, and the app connects at home but not away ([details](nested/echocat-connectivity.md#linux-only-let-potacat-ask-for-the-certificate))
3. Connect using the **MagicDNS hostname** shown in POTACAT's ECHOCAT panel (highlighted in green) with `https://` — the Tailscale `100.x.x.x` IP will not work, because the TLS certificate is issued only for the hostname
4. No port forwarding or firewall changes needed

See the [Connectivity & Pairing guide](nested/echocat-connectivity.md) for the full walkthrough, including the device-key expiry gotcha that makes Tailscale setups stop working after a couple of months.

### POTACAT Cloud Tunnel

The Cloud tunnel is the simplest remote path: your desktop opens an **outbound-only** tunnel to POTACAT Cloud and gets a personal address like `yourcallsign.potacat.com`. Because the connection is outbound from the shack, there is nothing to forward, no VPN to install, and no inbound firewall hole — it even works behind CGNAT (Starlink and many cellular ISPs), where port forwarding is impossible.

Security is layered: the tunnel accepts no inbound connections, pairing tokens are one-time-use, and requests are rate limited.

**One shack per Cloud address** (1.13.10). A Cloud account has one address, and it belongs to one desktop at a time. If a second desktop on the same account turns on the Cloud Tunnel, it asks first: **Use this shack instead**, **Keep the other shack** or **Cancel**. Turning the Cloud Tunnel off on one desktop leaves the address with the other. (Before 1.13.10, two desktops shared the address and split your phone's connections between them without saying so.)

**A Cloud address for each shack** (1.14.2). Each shack can have its own POTACAT Cloud address, up to 3 per membership, so ECHOCAT can switch between shacks over Cloud. Name the shack in **Settings > Cloud**.

## Share Your Rig

With POTACAT Cloud you can grant another operator timed access to your radio — a friend without HF at home, a club member, or a licensed guest anywhere in the world.

- You issue a **guest pass**: a four-word code (like `prague-plankton-potato-idaho`) that expires after a set number of hours
- You can cap **TX power**, and band privileges are enforced based on the guest's license class
- From 1.13.2, a guest can **tune to and listen to any spot**: a Technician can click a 20 m phone spot and listen. Transmit is what gets checked, against the guest's license class and the modes the pass allows. A refused key-down tells the guest why
- From 1.13.10, **a guest can operate the station and nothing else.** A guest can tune, transmit, change modes and levels, use the scope and log their own contacts. Anything else is refused with a message on their screen: raw CAT commands, your logbook, your Cloud account, your settings and Winlink mail
- From 1.13.10, **the pass's power cap is set on the radio.** When the guest starts, the radio is set to the pass's power cap, and your own power setting is put back when the pass ends. A radio that doesn't report its TX power over CAT can't transmit during a Guest Pass. That includes a Flex used through its CAT ports without the SmartSDR link
- With split on, a guest's transmission is checked against the frequency the radio will actually transmit on, not the dial
- From 1.14.0, **a guest is told why a transmission was refused**, in plain words, in their FT8 window, VFO window and log. When the refusal is because your radio isn't reporting its power, **you get a notice too**, *Guest Pass: your radio is not reporting its power, so the guest cannot transmit*, and the log says what to check: that **Settings > My Rigs** names the radio's exact model (and CI-V address on an Icom). On an Icom, see [CI-V pacing](nested/rig-ic-7300.md#ci-v-pacing-mode-or-power-never-reported)
- From 1.14.0, right after setting the radio to the pass's power cap, POTACAT asks the radio to report it, so the first transmission doesn't wait. A cap above the radio's [full power](nested/my-rigs.md#full-power-w) gives the radio's full power
- Normally the guest signs in with a **free POTACAT Cloud account**. That is how POTACAT knows the callsign to put on the air, and it provides the audit trail of who operated your station. In **Share my rig…**, under **Sign-in requirement**, you can tick **Allow without a POTACAT Cloud sign-in**. A guest with no sign-in has no verified callsign, so they can listen and log but not transmit
- From 1.14.5, **a valid pass is never shown as cancelled.** A guest using POTACAT as a remote is told what is happening, that the pass is still good, and POTACAT keeps trying: *Waiting: the owner is using the radio*, *standing by* when the guest's own phone has the radio, or *Couldn't check your pass just now. Trying again.* Only a pass that has ended or that you cancelled ends it, and leaving a session no longer uses up the pass. ECHOCAT Web shows the same, including when you pause the guest's session
- From 1.14.5, a pass that cannot be used says why in a sentence: a pass that belongs to another account, your own pass, or a pass made for another callsign
- From 1.14.6, **the Share Your Rig window shows who has the radio**, with three controls for you:
    - **Take the radio:** **Now** or **In 5 minutes**, with an optional message to the guest of up to 140 characters. A pending take can be called off with **Let** *call* **keep it**
    - **Give it back** hands the radio back to the guest
    - **Cancel pass** ends the pass once you confirm with **Yes, cancel the pass**. **Keep the pass** leaves it running
- From 1.14.6, when you have held the radio for 5 minutes with no transmitting, keying, tuning or mode change, the guest is told the radio is free and may press **Take the radio**. Nothing switches by itself. The old automatic 2-minute hand-back is gone
- From 1.14.6, a guest is told in plain words whether they are on the air, waiting and why, reconnecting, or the pass is over. A short Cloud hiccup no longer ends a pass. With two devices on one pass, **Use it here instead** moves it without dialling again
- From 1.14.6, a guest can use the station's own SDRs, switching between and tuning the ones you set up. Adding a new SDR is refused. A guest never receives SDR passwords saved inside an SDR address, or your full settings
- From 1.14.6, a contact a guest makes on your station goes on to the guest's own external logger, such as MacLoggerDX, through the guest's POTACAT
- From 1.14.7, a contact made on a lent station records the lending station's grid square, state and county, not the guest's home, and an activation contact takes the park's location. Such contacts go to LoTW in their own batch with that location
- Rig sharing requires the Cloud tunnel; Tailscale covers your own devices, but sharing means Cloud (or adding the guest to your Tailnet yourself)

> **Note:** The remote guest is the control operator and operates under **their own callsign**, per the usual remote-operation rules. Check the regulations that apply in your country.

## APRS in ECHOCAT Web

From 1.14.7, ECHOCAT Web has an **APRS** tab: the station list and map, listening on your radio, the iGate switch and an internet beacon. It cannot send messages or beacon on the radio. See [APRS](nested/aprs.md#in-a-browser-echocat-web).

## More Than One of Your Devices (Beta)

By default, the newest device to connect takes over the shack: connecting your laptop disconnects your phone, and the phone is told another device took over.

From POTACAT 1.13.0 you can keep several of your own devices on the shack at once. On the desktop, open **Settings > ECHOCAT > Advanced ECHOCAT settings** and turn on **Allow more than one of my devices at a time (beta)**. It is off by default. With it on, whoever keyed owns PTT until they let go, the shack's audio follows the device that asked for it last, and a Guest Pass is never shared.

## Security

### Who can reach this computer

> **New in POTACAT 1.13.10.**

**Settings > ECHOCAT > Who can reach this computer** sets where ECHOCAT listens. **Access** has three choices:

| Access | Who can reach the shack |
|---|---|
| **Local network and Cloud** (default) | Your local network, Tailscale and your POTACAT Cloud address, as before |
| **Cloud only** | Only your POTACAT Cloud address and Guest Passes. ECHOCAT is closed to your local network and Tailscale |
| **Off** | Nobody. ECHOCAT is closed completely |

Removing a device from the paired list closes all of its connections, including a second one when more than one device at a time is allowed.

### Certificate Warning (ECHOCAT Web)

On the LAN, ECHOCAT uses a self-signed TLS certificate. Your browser will warn you the first time — accept the certificate and it will be remembered for future sessions. Over Tailscale, ECHOCAT uses a real certificate issued for your MagicDNS hostname, so there's no warning — but that's also why you must connect by hostname, not IP.

### Password-protect your rig

Anyone who can open your ECHOCAT address (this PC on your network or Tailscale, port 7300) can see and control your radio. To require a password, open **Settings > ECHOCAT** and, directly under the ECHOCAT addresses, turn on **Password-protect your rig** (**Require a password to reach my ECHOCAT address**). Type a password or click **Random**. It is off when POTACAT is installed.

- **ECHOCAT Web** asks for the password before it shows the radio.
- **The ECHOCAT app** never asks you to type it. It receives the password inside the QR code, tap-to-pair or link you pair with.
- **The POTACAT Cloud tunnel** has its own sign-in.

Older app versions call this password the *access token*.

## Settings Reference

| Setting | Default | Description |
|---------|---------|-------------|
| Who can reach this computer | Local network and Cloud | **Local network and Cloud**, **Cloud only** or **Off** (1.13.10+). See [above](#who-can-reach-this-computer) |
| Port | 7300 | HTTPS/WebSocket server port |
| Password-protect your rig | Off | Require a password to reach the ECHOCAT address. The web page asks for it; the app gets it when pairing |
| PTT Safety Timeout | 180s | Auto-drop PTT after this many seconds |
| Enable Remote CW Keyer | Off | Allow CW keying from phone |
| CW Key Port | None | COM port for hardware DTR keying |
| Audio Input | None | RX audio device (radio → phone) |
| Audio Output | None | TX audio device (phone → radio) |
| Allow more than one of my devices at a time (beta) | Off | Under **Advanced ECHOCAT settings**. Lets several of your own devices share the shack (1.13.0+) |

## Troubleshooting

> **Note:** For pairing failures, Tailscale problems, "it worked for weeks and then stopped," and audio issues, see the dedicated [ECHOCAT Connectivity & Pairing guide](nested/echocat-connectivity.md). Still stuck? Update POTACAT on the shack PC, then [report a bug](community--support.md#report-a-bug) from POTACAT.

**Can't reach the ECHOCAT URL:**
- Make sure ECHOCAT is enabled (green indicator in POTACAT's connection bar)
- Verify your phone is on the same network as the PC (or both are on Tailscale, with **MagicDNS** and **HTTPS Certificates** enabled)
- Check that the port (default 7300) isn't blocked by your firewall
- If the URL shows a `169.254.x.x` address, Tailscale isn't actually running on the PC

**Certificate error won't go away:**
- On iOS Safari, you may need to tap "Show Details" then "visit this website"
- On Android Chrome, tap "Advanced" then "Proceed to [IP] (unsafe)"

**No audio:**
- Tap the Audio button on the phone and allow microphone access
- Check that the correct audio devices are selected in Settings > Radio
- On iOS, make sure your phone isn't on silent mode

**PTT not working:**
- Verify your radio's CAT connection is active (green dot in status bar)
- Check the PTT safety timeout hasn't expired (the phone will show a warning)
- Tap the STOP button and try again

**High latency / audio dropouts:**
- Use a 5 GHz Wi-Fi network instead of 2.4 GHz
- If using Tailscale remotely, latency depends on your internet upload speed at the shack
- Close other bandwidth-heavy applications

**Phone disconnects when screen locks:**
- On iOS, keep the browser in the foreground while operating
- The audio session helps keep the connection alive, so start audio before locking the screen
- On Android, disable battery optimization for your browser
- The native iOS/Android app keeps streaming with the screen locked — worth the upgrade if you operate this way often
