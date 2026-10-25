# Winlink Email

> **New in POTACAT 1.13.1.**

POTACAT sends and receives Winlink email from your shack: over the internet on Windows, Linux and Mac, over the radio with ARDOP (HF) on Windows, Linux and Mac, and with your own copy of VARA HF or VARA FM on Windows. There is nothing else to install. POTACAT runs [Pat](https://getpat.io/), the open-source Winlink client, in the background, and starts it the first time you use mail.

Open it from **More ▾ > Winlink Mail**. It is always in the menu, with nothing to turn on. The mail window has **Inbox**, **Outbox**, **Sent** and **Archive**, a composer with attachments, and a position report.

> **Note:** Winlink is amateur radio. The first time you send a message or start a session, POTACAT shows a short reminder: no business traffic, and nothing that needs privacy. The Winlink network is run by the Amateur Radio Safety Foundation.

## Your Winlink Account

You don't need to visit winlink.org. If your callsign has no Winlink account, POTACAT creates it. (Winlink accounts are created by a client program's first registration, not on the website, and POTACAT is that client.)

1. Open **Settings > Station > Winlink (email over radio)**.
2. Click **Check my account**. It tells you whether your callsign already has a Winlink account.
3. If it doesn't, choose a password (6 to 12 characters) and, if you like, a recovery email, then click **Create my Winlink account**.

**Already have an account?** Type its password into **Winlink password** and save.

**On your phone:** the ECHOCAT app has its own account setup under **Settings > Winlink**, so you can check or create the account from the phone instead.

From 1.13.2, the Winlink Mail window and ECHOCAT Web's **Mail** tab also open with **Set up your Winlink account** when no password is saved, and the password rule tells you what Winlink accepts before you send it.

## Sending and Receiving

Messages you write wait in the **Outbox** until the next **Send / Receive**. Choose how they go in **Send via**.

> **ARDOP and Internet are the modes to use, plus VARA HF or VARA FM if you have your own copy (Windows).** From 1.13.2, ARDOP works on macOS too.

### Over the internet

Pick **Internet (telnet)** in **Send via** and click **Send / Receive**. This works on Windows, Linux and Mac, and never uses the radio.

If you want mail fetched without asking, set **Check mail over the internet every … minutes** in Settings. That check uses the internet only, never the radio. A radio session always starts from your own **Send / Receive**.

### Over the radio with ARDOP

1. Pick **ARDOP (radio)** in **Send via**.
2. Choose a **Band**, then pick a gateway from the list. The list is sorted nearest first.
3. The radio tunes to the gateway straight away, and a waterfall with a **Busy** / **Clear** badge shows whether someone is already using the frequency.
4. When it reads **Clear**, click **Send / Receive**.

POTACAT handles the radio for the whole session:

- It moves the radio to data mode, keys it, and puts the dial back where it was when the session ends.
- **Power**, **PWR** and **SWR** sit on the session line while you transmit.
- The SWR guard stops a session that is transmitting into a bad match.
- A session ends after the time limit you set (**End a radio session after … minutes** in Settings). A stuck session also ends after 3 minutes with no progress, and the transmitter is released if it stays keyed for 30 seconds.

### Over the radio with VARA (Windows, your own copy)

> **New in POTACAT 1.13.2.**

VARA is EA5HVK's modem. You install and license it yourself; POTACAT doesn't install or download any part of it. Without a licence, VARA runs at reduced speed.

**What to install first:**

1. **VARA HF**, and **VARA FM** if you want VHF/UHF, from [rosmodem.wordpress.com](https://rosmodem.wordpress.com/).
2. **Only for a FlexRadio on Flex Direct or an Icom over the network:** two free virtual audio cables from [vb-audio.com/Cable](https://vb-audio.com/Cable/), **VB-CABLE** and the **Hi-Fi Cable** (or the donation A+B pack). Run each installer as administrator, then reboot. A radio with a USB sound card needs no cable; VARA uses the sound card directly.

**Then, in Settings > Station > Winlink (email over radio) > VARA (your own copy, Windows):**

1. Tick **Use VARA HF** or **Use VARA FM**.
2. Click **Set up VARA HF for me** (or **Set up VARA FM for me**). POTACAT configures VARA for the active radio, including its sound card or the cables, PTT (set to VOX) and the port. It then starts VARA and checks that VARA opened the devices. VARA is configured again whenever a session starts it or you switch radios.
3. Leave **Start VARA for me when a session needs it** ticked. VARA starts once and stays open between sessions; POTACAT never closes it.

If you run both, set VARA FM to port **8310** in VARA FM's own settings, because both programs ship on 8300.

**Sending:** pick **VARA HF (radio, your own VARA)** or **VARA FM (VHF/UHF radio, your own VARA FM)** in **Send via**, choose a gateway, and click **Send / Receive**. POTACAT levels the audio both ways. The radio audio VARA hears is trimmed before it reaches the red, and VARA's transmit audio is raised to full scale, so the power you set is the power that goes out. The Mail window shows both levels during a session (**to modem … · from modem …**).

A session you stop stays stopped, and a new session waits for the last one to hang up.

### Also listed, not recommended yet

**Send via** also lists **Packet (VHF/UHF radio)**, which uses the Dire Wolf modem built into POTACAT, and **Mercury (radio, experimental)**, which stays greyed out until Mercury is turned on in **Settings > Station**. Neither is recommended yet. Use ARDOP or Internet.

## Audio for Radio Sessions

- **FlexRadio on Flex Direct, or an Icom over the network:** ARDOP needs no sound card and no DAX. VARA needs the two virtual audio cables described above.

Radio sessions need a radio with CAT control, because POTACAT tunes and keys it.

From 1.13.2, ARDOP and packet take their audio over POTACAT's own link to the radio on every system, so there are no sound devices to pick by hand. VARA has its own audio setup (see [above](#over-the-radio-with-vara-windows-your-own-copy)).

## Spot Yourself on POTA by Winlink

With no internet in the park, you can still spot yourself on POTA through Winlink. [POTA Spotter](https://potaspot.tdod.org/) is a free service that turns an email into a POTA self-spot. Thanks to Charlie, W7RTA, who found that it works from POTACAT.

### The spot buttons

> **New in POTACAT 1.13.3.**

POTACAT fills in the spot for you:

- **In an activation**, click **Spot by Winlink**, beside **Spot**. The button appears once you have accepted the Winlink reminder in Winlink Mail. Winlink Mail opens with the spot filled in: your callsign, every POTA park of the activation, and the frequency and mode that **Spot** uses.
- **In Winlink Mail**, click **POTA spot**, beside **Position report**. It fills the spot from your activation and the radio's frequency and mode.

Check the line, add a comment after the mode if you like, then click **Put in Outbox** and **Send / Receive**. Nothing goes out by itself. For an n-fer, POTACAT sends one message per park.

If POTACAT doesn't know the park or the frequency yet, the line shows **PARK** or **FREQ**, with a note saying what to fill in. **Put in Outbox** refuses the line until you do. USB and LSB are sent as SSB, and data modes as FT8, or as the mode JTCAT is running.

### By hand

1. In the Winlink Mail window, write a new message to **spot@pota.tdod.org**. The subject can be anything.
2. In the body, put one line in this form:

   `!CALLSIGN POTA PARK FREQUENCY MODE COMMENTS`

   The frequency is in MHz, and the comments are optional. For example:

   `!W7RTA POTA US-0786 14.0675 CW CQ POTA`

3. Click **Put in Outbox**, then **Send / Receive**, over ARDOP or VARA from the field.

The spot shows on POTA as coming from the activator. **To respot**, for example after you change band, send another message with the new frequency. **QRT** as the comment marks you QRT. The service reads one line per message, so for an n-fer send one message per park. Winlink can take a few minutes to deliver, so allow time for the spot to appear.

To test it, use **K-TEST** as the park, for example `!W7RTA POTA K-TEST 14.000 CW TEST SPOT`. A real park posts a real public spot.

> **Note:** POTA Spotter isn't run by POTACAT. Questions about the service go to the address on [its page](https://potaspot.tdod.org/).

## From Your Phone or a Browser

The ECHOCAT app and ECHOCAT Web both have a **Mail** tab with the same folders, composer, gateway list, waterfall and **Send / Receive**. The shack PC holds the mailbox and keys the radio, so the desktop must be on POTACAT 1.13.1 or later. Winlink is for the station owner only: the shack refuses mail from a Guest Pass. A VARA session started from the phone shows "Starting VARA HF on the shack PC" while VARA comes up, and a failure says what is wrong on the shack PC. See [ECHOCAT](../echocat.md).

> **Note:** A desktop that is [driving a remote shack](remote-desktop.md) can't start a radio session. Start radio sessions on the shack PC.

## Privacy

What POTACAT stores and sends for Winlink is described at [potacat.com/privacy-terms.html#winlink](https://potacat.com/privacy-terms.html#winlink).
