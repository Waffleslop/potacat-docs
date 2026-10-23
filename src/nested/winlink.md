# Winlink Email

> **New in POTACAT 1.13.1.**

POTACAT sends and receives Winlink email from your shack: over the internet on Windows, Linux and Mac, and over the radio with ARDOP (HF) or packet (VHF/UHF) on Windows and Linux. There is nothing else to install. POTACAT runs [Pat](https://getpat.io/), the open-source Winlink client, in the background, and starts it the first time you use mail.

Open it from **More ▾ > Winlink Mail**. It is always in the menu, with nothing to turn on. The mail window has **Inbox**, **Outbox**, **Sent** and **Archive**, a composer with attachments, and a position report.

> **Note:** Winlink is amateur radio. The first time you send a message or start a session, POTACAT shows a short reminder: no business traffic, and nothing that needs privacy. The Winlink network is run by the Amateur Radio Safety Foundation.

## Your Winlink Account

Open **Settings > Station > Winlink (email over radio)**.

- **New to Winlink?** Click **Check my account**. It tells you whether your callsign already has a Winlink account. If it doesn't, choose a password (6 to 12 characters) and, if you like, a recovery email, then click **Create my Winlink account**.
- **Already have an account?** Type its password into **Winlink password** and save.

## Sending and Receiving

Messages you write wait in the **Outbox** until the next **Send / Receive**. Choose how they go in **Send via**.

### Over the internet

Pick **Internet (telnet)** in **Send via** and click **Send / Receive**. This works on Windows, Linux and Mac, and never uses the radio.

If you want mail fetched without asking, set **Check mail over the internet every … minutes** in Settings. That check uses the internet only, never the radio. A radio session always starts from your own **Send / Receive**.

### Over the radio with ARDOP (Windows and Linux)

1. Pick **ARDOP (radio)** in **Send via**.
2. Choose a **Band**, then pick a gateway from the list. The list is sorted nearest first.
3. The radio tunes to the gateway straight away, and a waterfall with a **Busy** / **Clear** badge shows whether someone is already using the frequency.
4. When it reads **Clear**, click **Send / Receive**.

POTACAT handles the radio for the whole session:

- It moves the radio to data mode, keys it, and puts the dial back where it was when the session ends.
- **Power**, **PWR** and **SWR** sit on the session line while you transmit.
- The SWR guard stops a session that is transmitting into a bad match.
- A session ends after the time limit you set (**End a radio session after … minutes** in Settings). A stuck session also ends after 3 minutes with no progress, and the transmitter is released if it stays keyed for 30 seconds.

### Packet (VHF/UHF, Windows and Linux)

Pick **Packet (VHF/UHF radio)** in **Send via** to reach a packet gateway through the Dire Wolf modem built into POTACAT. Choose the band and gateway the same way as for ARDOP. **Packet speed** (1200 or 9600) is set in Settings.

### Mercury (experimental)

**Send via** also lists **Mercury (radio, experimental)**. It stays greyed out until Mercury is turned on in **Settings > Station**, and few gateways run it yet. Use ARDOP for HF.

## Audio for Radio Sessions

- **FlexRadio on Flex Direct, or an Icom over the network:** ARDOP needs no sound card and no DAX. The modem's audio travels over POTACAT's own link to the radio.
- **A radio with a USB sound card:** POTACAT uses the same capture and playback devices as your FT8, and asks only when it can't tell. To change them, use **Find the radio's sound devices** in the Winlink settings. They are saved per radio.
- **Packet** needs a sound device: the radio's USB sound card, or DAX on a Flex that isn't on Flex Direct.

Radio sessions need a radio with CAT control, because POTACAT tunes and keys it. They aren't available on macOS yet.

## From Your Phone or a Browser

ECHOCAT Web has a **Mail** tab with the same folders, composer, gateway list, waterfall and **Send / Receive**. The shack PC holds the mailbox and keys the radio. See [ECHOCAT](../echocat.md).

The ECHOCAT app's Mail tab is coming in an app update.

> **Note:** A desktop that is [driving a remote shack](remote-desktop.md) can't start a radio session. Start radio sessions on the shack PC.

## Privacy

What POTACAT stores and sends for Winlink is described at [potacat.com/privacy-terms.html#winlink](https://potacat.com/privacy-terms.html#winlink).
