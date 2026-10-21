# Run Your Shack from Another POTACAT

> **New in POTACAT 1.13.0.** Both computers need 1.13.0 or later.

A second POTACAT — on a laptop, or a PC at work — can operate the radio attached to your shack PC, the same way the ECHOCAT phone app does. It works over the same Wi-Fi, over Tailscale, or over POTACAT Cloud.

The shack PC keeps running everything that touches the radio: CAT, the FT8 and JS8 engines, SSTV, the CW keyer. The second POTACAT is the screen, keyboard, speaker and microphone.

## What You Need

- **POTACAT on the shack PC**, connected to the radio, with **ECHOCAT** turned on (see [ECHOCAT — Quick Start](../echocat.md#quick-start))
- **POTACAT on the second computer**
- **A connection path** between them: the same network, Tailscale, or POTACAT Cloud — the same three paths the phone app uses (see [Connectivity & Pairing](echocat-connectivity.md))

## Pairing

On the second POTACAT, open **More ▾ > Remote Radios…**. Then pair in whichever way suits you:

- **Same network:** on a fresh install, the setup screen lists the shacks it finds on your network. Click one, then approve the request on the shack.
- **POTACAT Cloud:** sign in to the same Cloud account on both computers. The second computer lists your shacks; click **Pair**.
- **A link:** on the shack, open **Settings > ECHOCAT** and click **Pair my device…** on the ECHOCAT card, then copy the link. Paste it into the box at the top of **Remote Radios** on the second computer.

Then click **Connect**. The status bar shows the shack's name, its radio, the connection in use (**LAN**, **Tailscale** or **Cloud**) and the round-trip time.

## What Works

### The radio

- Tuning from spots and the map, and the **VFO window**
- Mode and filter
- The rig controls: NB, ATU, preamp and attenuator, DSP, power, split, VFO A/B and lock
- [Rig presets](../radio-setup.md#rig-presets) and custom CAT buttons
- Switching between the shack's radios — click the **RMT** pill in the status bar

### Audio

- The shack's receive audio plays on this computer.
- Hold **HOLD TO TALK** — or a key you choose — and your microphone goes to the radio.
- Choose the speaker, microphone and push-to-talk key in **Settings > ECHOCAT > Driving a remote shack**.
- Volume and mute sit next to **HOLD TO TALK**.

### FT8, FT4, FT2, WSPR, PSK31 and JTTY

- Open the JTCAT window as usual. It runs the shack's decoder and transmitter.
- QSOs are logged in **this computer's** logbook.
- Multi-band (multi-slice) FT8 runs only on the shack PC.

### CW

- Typed CW, CW macros and live typing go to the shack.
- A paddle plugged into this computer keys the shack's radio.
- The shack must have **Settings > ECHOCAT > Remote CW Keyer** turned on. See [Remote CW Keying](remote-cw.md).

### JS8

The JS8 window runs the shack's JS8: conversations, band activity, heartbeat, messages, and logging into this computer's logbook. Opening the window starts JS8 on the shack; closing it stops JS8 there.

### SSTV

- Compose and send a picture from this computer; the shack transmits it.
- Received pictures appear when they are complete (a progress bar shows them coming in), and are saved in this computer's gallery too.
- Redecode and multi-slice SSTV run only on the shack PC.

### Voice macros

The buttons are the shack's recorded macros, played into the shack's radio.

### Band scope

The shack's band scope, from an FT-710 or a separate SDR.

### Activating

Start an activation on this computer as usual. The shack learns the park, so FT8 contacts are logged with it.

### Everything else

Spots, the map, the logbook, cloud sync, LoTW and QRZ uploads, and DXCC tracking all run natively on this computer.

## What Doesn't Work from the Second Computer

- **Station Setup** — run it on the shack PC.
- **Mercury**
- **Idle Mode** (idle receive) — it is the shack's own setting, so set it on the shack PC.

Each of these is greyed out with a one-line reason while you are connected to a shack.

## More Than One Device at a Time

**By default, the newest device takes over.** Connecting the laptop disconnects your phone, and the phone is told that another device took over.

To keep both connected, on the shack open **Settings > ECHOCAT > Advanced ECHOCAT settings** and turn on **Allow more than one of my devices at a time (beta)**. With it on:

- Whoever presses PTT holds the radio until they let go.
- Each device is told when another one tunes.
- The shack's audio goes to the device that asked for it last. The others show **AUDIO ON ANOTHER DEVICE**; click **Operate from this device** (beside **HOLD TO TALK**) to take it.

A [Guest Pass](../echocat.md#share-your-rig) always has the radio to itself.

> **Note:** A desktop that is driving a shack can't pass the radio on to a phone. Connect the phone to the shack directly.

## If Something Is Off

**The chip in the status bar says what is happening:**

- **connecting** or **reconnecting** — POTACAT is trying the LAN, then Tailscale, then Cloud.
- **re-pair** — the shack refused the pairing (it expired, or was removed on the shack). For a Cloud-linked shack, click **Re-pair** in Remote Radios. Otherwise, click **Pair my device…** on the shack and paste the fresh link.
- **NO AUDIO** — the link is up, but no audio has arrived for 10 seconds. Check the shack's audio source, and that ECHOCAT is on there.

**While the link is down, nothing goes to the radio by accident.** A tune or a PTT press is refused with *"The remote shack is not connected right now."*

**To go back to this computer's own radio,** click the **RMT** pill, then **Use this PC's radio**. Or click **Use local rig** in Remote Radios.

For connection problems that aren't specific to desktop-to-desktop — Tailscale settings, firewalls, Cloud sign-in — see [Connectivity & Pairing](echocat-connectivity.md).
