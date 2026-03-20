# ECHOCAT — Remote Phone Control

ECHOCAT turns your phone into a wireless remote for your POTACAT-connected radio. Tune spots, transmit, stream audio, send CW, log QSOs, and even run POTA activations — all from a mobile browser over a secure connection.

## What You Need

- **POTACAT** running on your shack PC, connected to your radio
- **A phone or tablet** with a modern browser (Safari on iOS, Chrome on Android)
- **Network connectivity** between the two — either your home Wi-Fi (for local use) or **Tailscale** (for remote access away from the shack)

## Quick Start

### 1. Enable ECHOCAT on the Desktop

Open POTACAT and click the **gear icon** in the top bar to open Quick Settings. Toggle **ECHOCAT** on. You'll see:

- A URL (e.g., `https://192.168.1.50:7300`)
- A 6-character token (e.g., `A1B2C3`)

If you have Tailscale installed, the Tailscale IP is shown with a green label — use that IP for remote access.

You can also configure ECHOCAT from **Settings > ECHOCAT**, where you can change the port (default 7300), regenerate the token, set the PTT safety timeout, and select audio devices.

### 2. Open ECHOCAT on Your Phone

1. Open your phone's browser and navigate to the URL shown in POTACAT
2. You'll see a certificate warning (ECHOCAT uses a self-signed TLS certificate) — tap **Advanced** > **Proceed** to accept it
3. Enter the 6-character token and tap **Connect**

That's it — you're connected. You'll see the spot list, a frequency display, and the mode badge at the top.

### 3. Select Audio Devices

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

### Audio

Tap the **Audio** button to start streaming. Your phone will ask for microphone permission — this is needed for TX audio.

- **RX audio** streams from your radio to your phone speaker/earpiece
- **TX audio** streams from your phone microphone to the radio when PTT is held
- Tap **Vol** to cycle through gain levels (1x, 2x, 3x) if RX audio is too quiet

> **iOS note:** Keep ECHOCAT in the foreground or use the Audio button to maintain the connection. iOS aggressively suspends background WebSocket connections.

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

### Rotor Control

If you have PSTRotator configured in POTACAT, a rotor toggle appears in the radio controls section. When enabled, tuning a spot automatically sends the bearing to your rotator.

## CW from Your Phone

ECHOCAT includes a full CW keyer that lets you send CW from your phone's touchscreen or a Bluetooth MIDI paddle.

### Enable CW

1. In POTACAT desktop Settings > ECHOCAT, check **Enable CW Keyer**
2. On your phone, the CW panel appears when you're in CW mode

### CW Panel Controls

- **WPM** — adjust sending speed (5–50 WPM)
- **Keyer mode** — Iambic B, Iambic A, or Straight Key
- **Sidetone** — adjustable frequency (400–900 Hz) and volume
- **5 macro buttons** — programmable CW messages (default: CQ, 599, 73, AGN, TU). Customize the labels and text in POTACAT's desktop settings.
- **Free text field** — type any text and send it as CW

### CW Keying Methods

ECHOCAT supports three keying methods that can work simultaneously:

1. **Text macros (KY command)** — Tap a macro button and the radio's internal keyer sends the text. Best for programmed messages with clean keying. Requires radio firmware support (QMX firmware 1\_00\_021+).

2. **Paddle CW (TX/RX keying)** — Touch the on-screen paddle or use a Bluetooth MIDI paddle. Your phone sends paddle contact events over WebSocket, POTACAT's iambic keyer generates the timing, and TX/RX commands key the radio. Preserves your sending rhythm.

3. **Hardware DTR keying** — A dedicated USB-to-serial adapter wired to your radio's key jack. Best for absolute timing precision. See the [Remote CW Setup Guide](/remote-cw-setup) for wiring details.

> **Sidetone:** For paddle CW and DTR keying, your phone generates local sidetone via its speaker — the radio's sidetone is not used since TX/RX keying bypasses the radio's internal keyer.

## FT8 / Digital Modes (JTCAT)

ECHOCAT integrates with POTACAT's JTCAT feature for remote FT8/FT4 operation.

Tap the **FT8** tab on your phone to access:

- **Band selection** (80m–6m) with one-tap band changes
- **Mode selector** (FT8, FT4, FT2)
- **Decode log** — live scrolling list of decoded stations
- **TX controls** — enable TX, call CQ, reply to stations
- **Waterfall** — live spectrum display streamed from the desktop
- **Auto QSO sequencing** — JTCAT handles the exchange sequence; you just pick who to call

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
- Your contact list shows at the bottom of the activation view

### Re-spotting

When you log a QSO during an activation, ECHOCAT can automatically re-spot you on POTA/SOTA/WWFF. Configure your re-spot comment template in POTACAT's desktop settings (e.g., `{rst} in {QTH} 73 {mycallsign} via POTACAT`).

### Export

Tap **Export ADIF** to generate an ADIF file of your activation contacts. Past activations are saved and viewable with individual map views showing your QSO locations.

## Club Station Mode

For multi-operator club stations, ECHOCAT supports authenticated access with license privilege enforcement.

### Setup

1. In POTACAT Settings > ECHOCAT, enable **Club Station Mode**
2. Point it to a `club_users.csv` file with columns for callsign, password, license class, and rig access
3. Each member logs in with their callsign and password

### How It Works

- Members can only tune frequencies within their license class privileges (e.g., a US Technician can't tune 80m SSB)
- Rig access can be restricted per member
- The OPERATOR field in logged QSOs is set to the individual member's callsign
- All actions (logins, tunes, PTT, rig switches) are written to an audit log

## Network & Security

### Local Network

On your home Wi-Fi, your phone can reach POTACAT directly at its LAN IP address. No special setup needed beyond enabling ECHOCAT.

### Remote Access with Tailscale

For operating away from the shack:

1. Install **Tailscale** (free) on both your shack PC and your phone
2. Sign in on both devices with the same account
3. Use the **Tailscale IP** shown in POTACAT's ECHOCAT panel (highlighted in green)
4. No port forwarding or firewall changes needed — Tailscale creates an encrypted tunnel

### Certificate Warning

ECHOCAT generates a self-signed TLS certificate that includes all your local and Tailscale IP addresses. Your browser will warn you the first time — accept the certificate and it will be remembered for future sessions. The certificate regenerates once per year.

### Token Authentication

The 6-character hex token prevents unauthorized access. You can regenerate it at any time from the desktop settings. Share it only with people you want to grant radio access.

## Settings Reference

| Setting | Default | Description |
|---------|---------|-------------|
| Enable ECHOCAT | Off | Start the ECHOCAT server |
| Port | 7300 | HTTPS/WebSocket server port |
| Require Token | On | Require token authentication |
| Token | Auto-generated | 6-character hex authentication token |
| PTT Safety Timeout | 180s | Auto-drop PTT after this many seconds |
| Enable CW Keyer | Off | Allow CW keying from phone |
| CW Key Port | None | COM port for hardware DTR keying |
| Audio Input | None | RX audio device (radio → phone) |
| Audio Output | None | TX audio device (phone → radio) |

## Troubleshooting

**Can't reach the ECHOCAT URL:**
- Make sure ECHOCAT is enabled (green indicator in POTACAT's connection bar)
- Verify your phone is on the same network as the PC (or both are on Tailscale)
- Check that the port (default 7300) isn't blocked by your firewall

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
