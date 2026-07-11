# ECHOCAT Connectivity & Pairing

Getting your phone talking to your shack PC is the one part of [ECHOCAT](../echocat.md) that involves networking — and networking is where most people get stuck. This page is the plain-English version: which connection path to pick, how to set it up, and what every error message actually means.

> **Note:** Before troubleshooting anything, **update POTACAT Desktop**. The app is a remote control for the desktop, and most connection fixes ship on the desktop side.

## Pick Your Path

| Path | Use it when | Needs Tailscale? | Needs port forwarding? |
|------|-------------|------------------|------------------------|
| **Same LAN** | You're at home on the same Wi-Fi as the shack PC | No | No |
| **POTACAT Cloud** | You want remote access with the least setup, or you're behind CGNAT (Starlink, many cellular ISPs), or you want to share your rig | No | No |
| **Tailscale** | You want free remote access forever and don't mind a little one-time setup | Yes | No |

The one thing all three have in common: **you never port-forward anything.** (See [why below](#why-you-cant-just-port-forward-7300).)

You don't have to choose forever, either — the app tries all available paths at connect time and uses the fastest, switching automatically as you move between networks. The indicator at the top of the app shows the active path (**LAN**, **TAIL**, or **CLOUD**) and the latency in milliseconds.

## Path 1: Same Wi-Fi (LAN)

Nothing to configure. Enable ECHOCAT on the desktop, pair the app (or open the URL in a browser), and go. This is the fastest, lowest-latency path.

The only common snag is on iPhone — iOS blocks local-network access until you allow it. See [iOS: QR scans but nothing happens](#ios-qr-scans-but-nothing-happens).

## Path 2: POTACAT Cloud

The "easy button." Your desktop opens an **outbound-only** tunnel to POTACAT Cloud and gets a personal address like `yourcallsign.potacat.com`. Because the shack PC dials *out*, there is:

- no Tailscale or VPN to install
- no port to forward
- no inbound firewall hole
- no problem with CGNAT — it works on Starlink and cellular connections where port forwarding is physically impossible

Cloud is also the only path that supports [sharing your rig](../echocat.md#share-your-rig) with other operators.

> **Note:** If the desktop's verbose log shows `cloudflared ... Failed to refresh DNS`, the Cloud tunnel service itself is down — that one isn't your setup.

## Path 3: Tailscale (Full Walkthrough)

Tailscale is a free personal VPN that makes your phone and shack PC act like they're on the same network, wherever you are. It takes about ten minutes to set up correctly — and two of those minutes prevent roughly 90% of all failures.

### Step 1: Install Tailscale on both devices

Install Tailscale on the shack PC and on your phone, and sign in to the **same account** on both. Both devices must show as connected on the same Tailnet.

### Step 2: Enable the two settings everyone misses

This is the big one. Log in to the Tailscale admin console and open the DNS page at `https://login.tailscale.com/admin/dns`. Enable **both** of these:

1. **MagicDNS**
2. **HTTPS Certificates**

If pairing fails with **"Pairing request failed: Network request failed"**, it is almost always because one or both of these are off. Turn them on, update POTACAT Desktop, regenerate the pairing QR, and try again.

> **Tip:** Tailscale's own guide to these settings: `https://tailscale.com/docs/how-to/set-up-https-certificates`

### Step 3: Use the hostname, not the IP

Always connect using the **green MagicDNS URL** shown in POTACAT's ECHOCAT panel, with `https://` — something like `https://shack-pc.tailXXXX.ts.net:7300`.

Do **not** type the Tailscale `100.x.x.x` IP into your browser. Here's why: public certificate authorities are not allowed to issue TLS certificates for CGNAT addresses (the `100.64.0.0/10` range Tailscale uses) or private IPs. So the certificate Tailscale issues for your PC is valid **only for the MagicDNS hostname** — connect by IP and the secure connection fails before ECHOCAT ever sees it.

> **Note:** The very first connection can take about 30 seconds while the TLS certificate is issued. That's normal — it only happens once.

### Step 4: Stop it from expiring

Tailscale device keys expire after roughly **60–90 days** by default. This is the classic "it worked perfectly for two months and then died out of nowhere."

Prevent it: in the Tailscale admin console, open each device's **⋯** menu and select **Disable key expiry** for your shack PC and phone. If it has already expired, just re-authenticate Tailscale on the affected device.

### Tailscale quick diagnostics

| Symptom | What it means / what to do |
|---------|---------------------------|
| POTACAT shows a `169.254.x.x` URL | Tailscale isn't actually running on the PC — even if Task Manager says otherwise. Restart Tailscale. |
| "Pairing request failed: Network request failed" | **MagicDNS** or **HTTPS Certificates** not enabled (Step 2). Also update the desktop and regenerate the QR. |
| "A server with the specified hostname could not be found" | Tailscale isn't connected on the *phone*, or the QR is stale — regenerate the QR after any network change. |
| Worked for weeks, suddenly stopped | Device key expiry (Step 4), or Tailscale disconnected on one end. |
| Pairing only works when Tailscale is *off* | MagicDNS can occasionally interfere with pairing on some networks. Temporarily disable Tailscale to pair, or switch to the Cloud path. |
| Higher latency than expected | Tailscale may be routing through its relay servers. Some users report that enabling a direct connection shaved 35–55 ms off the ping. |

## Why You Can't Just Port-Forward 7300

It's tempting: forward port `7300` on your router and skip the VPN. It won't work, and it's not your fault.

The control connection does use port `7300`, but the **audio stream uses WebRTC on dynamic UDP ports** — different ports every session, and the UDP flow is initiated from the remote end, so your router's "established connections" rules never match it. You'd get a page that loads and a radio you can tune, but no audio.

Any real VPN solves this by putting both devices on one virtual network. Tailscale is the recommended one, but some users run **WireGuard** or **ZeroTier** successfully.

> **Warning:** Third-party VPNs can also *break* things — ZeroTier and similar VPNs have interfered with app pairing for some users, and at least one commercial VPN blocked the UDP audio stream entirely. If pairing or audio fails and you run a VPN other than Tailscale, try disabling it first.

## Pairing the App

### Version rules (read this first)

- **The newest app needs the newest desktop.** New app features generally ship with a matching POTACAT Desktop release — always update the desktop first.
- **QR pairing requires desktop v1.9.2 or later.** Older desktops can't pair with current app builds.
- **App updates arrive over-the-air**: in the app, go to **Settings > About > Check for updates**, then fully close and reopen the app. The build number won't change after an OTA update — that's normal.
- **OTA updates only target the newest store build.** If your App Store / Google Play version is old, you silently stop receiving fixes — update from the store occasionally even if the app "seems fine."

### iOS: QR scans but nothing happens

If the iPhone scans the QR and then... nothing — no error, no pairing — iOS is silently blocking local-network access:

1. Open iOS **Settings > ECHOCAT** and turn **Local Network** ON (also check **Settings > Privacy & Security > Local Network**)
2. Force-quit the ECHOCAT app
3. Re-pair

### Stuck in an approval loop

If the app loops forever at "asking for approval," an old pairing is in the way. Open your **POTACAT Cloud devices list**, revoke any stale or duplicate devices, and pair again.

### QR scans but the connection never finishes

Update POTACAT Desktop. Early versions choked when pushing a very large QSO log to the phone during pairing; current desktops cap that transfer. Note that with very large logbooks, the phone won't show per-call QSO history — spots and worked-parks still sync.

### Tap-to-pair buttons do nothing (Android)

Some users report that the Approve/Deny dialog from Android network auto-discovery doesn't respond. Workaround: use the QR code or open the pairing URL directly instead.

## Desktop Updates Won't Install (POTACAT Launcher)

If a POTACAT Desktop update fails with an "app is running" error even though you closed POTACAT, the culprit is the **POTACAT Launcher** — the separate background daemon (port `7301`) that lets the app start POTACAT remotely. It can hold a file lock on the installation.

Fix: open **Task Manager**, end the **POTACAT Launcher** process, and run the update again.

## Audio Troubleshooting

### Echo, or you hear yourself delayed

Echo is almost always a **wrong audio device**. In POTACAT **Settings > Radio**, set the ECHOCAT audio input and output to your rig's own USB sound device explicitly — for example `USB Audio CODEC` on an Icom IC-7300, or `FT-710 USB Audio`. "System Default" only works if the radio's USB audio happens to be the OS default device, which it usually isn't.

Two more echo sources:

- **Phone speaker feedback** — the phone mic is live during receive, so speaker audio loops back. Use headphones or earbuds.
- **Network strain** — check the latency figure at the top of the app. Above roughly `300 ms`, expect delayed self-echo and choppy TX audio; that's the connection, not the settings.

### No audio at all

Work down this list:

1. Tap the **Audio** button — then tap it **again** (a single tap doesn't always start the stream)
2. Allow **microphone permission** when the phone asks — TX audio needs it
3. Check the audio **input and output devices** in POTACAT — the computer won't pick the radio's audio by default
4. On iOS, check the **silent/ring switch**
5. If you're running a VPN other than Tailscale, it may be blocking the UDP audio stream — disable it and retry
6. On Android, make sure the app is up to date — old builds had broken speaker routing

### RX audio doesn't come back after PTT

A known quirk on some devices: tap the **Spkr** button twice, or use the **Restart Audio** button to reset the stream.

> **Tip:** To hear what the radio is putting out from the shack PC itself, click **VFO** and then the speaker icon in POTACAT Desktop.
