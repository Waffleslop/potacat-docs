# Winlink Email

> **New in POTACAT 1.13.1.**

POTACAT sends and receives Winlink email from your shack: over the internet on Windows, Linux and Mac, over the radio with ARDOP (HF) and packet, and with your own copy of VARA HF or VARA FM. There is nothing else to install. POTACAT runs [Pat](https://getpat.io/), the open-source Winlink client, in the background, and starts it the first time you use mail.

Open it from **More ▾ > Winlink Mail**. It is always in the menu, with nothing to turn on. The mail window has **Inbox**, **Outbox**, **Sent**, **Archive** and, from 1.14.5, **Deleted**, a composer with attachments, and a position report.

> **Note:** Winlink is amateur radio. The first time you send a message or start a session, POTACAT shows a short reminder: no business traffic, and nothing that needs privacy. The Winlink network is run by the Amateur Radio Safety Foundation.

## Your Winlink Account

You don't need to visit winlink.org. If your callsign has no Winlink account, POTACAT creates it. (Winlink accounts are created by a client program's first registration, not on the website, and POTACAT is that client.)

1. Open **Settings > Station > Winlink (email over radio)**.
2. Click **Check my account**. It tells you whether your callsign already has a Winlink account.
3. If it doesn't, choose a password (6 to 12 characters) and, if you like, a recovery email, then click **Create my Winlink account**.

**Already have an account?** Type its password into **Winlink password** and save.

**On your phone:** the ECHOCAT app has its own account setup under **Settings > Modes > Winlink**, so you can check or create the account from the phone instead.

From 1.13.2, the Winlink Mail window and ECHOCAT Web's **Mail** tab also open with **Set up your Winlink account** when no password is saved, and the password rule tells you what Winlink accepts before you send it.

## Filing, Deleting and Replying

> **New in POTACAT 1.14.5.**

- **Archive.** A message in the Inbox or Sent has an **Archive** button. In the Archive folder, a button moves it back to where it came from.
- **Deleted.** **Delete** moves a message to the **Deleted** folder instead of erasing it, so it no longer asks first. In Deleted, **Restore** puts it back in the folder it came from, and **Delete for good** removes it after you confirm on the button itself. To save the attachments of a deleted message, restore it first.
- **Deleted empties itself** after 7, 30 or 90 days, or Never. The default is 30. Choose at the top of the Deleted folder, or with **Empty the Deleted mail folder after** in **Settings > Station > Winlink**.
- **Reply all.** A **Reply all** button sits next to **Reply** when a message went to anyone besides you and the sender. The sender goes in To, and everyone else in Cc, without your own address and without anyone twice.
- **How a message went out.** A message in Sent, Archive or Deleted shows one line under its header, for example *Sent 13 Nov 2026 at 14:32 UTC via W5ABC on 7.102 MHz (ARDOP).* or *Sent 13 Nov 2026 at 14:32 UTC over the internet.* Only messages sent from 1.14.5 on have it.

## Winlink Forms

> **New in POTACAT 1.14.7.** Forms are not yet in the ECHOCAT app or ECHOCAT Web.

The Winlink Standard Forms are the forms Winlink Express uses: the Winlink Check-in for nets such as Winlink Wednesday, the ICS-213 General Message, and about 150 more (ICS, Red Cross, radiogram and state forms). A form message is an ordinary Winlink message plus an attachment that Winlink Express and Pat show as the filled form.

### Get the forms

POTACAT does not ship the forms, and never downloads them by itself.

1. In Winlink Mail, press **Forms**. The first time it says *No forms on this computer yet. Pat gets the Winlink Standard Forms (about 3 MB) from getpat.io.*
2. Press **Get the standard forms**. Pat downloads them once onto this computer. This one step needs the internet.

Afterwards the panel shows the count and the version, for example *153 forms, Winlink Standard Forms version 1.1.22.0.*, and the button reads **Check for newer forms**. If getpat.io cannot be reached, it says *Pat could not reach getpat.io, where it gets the Winlink Standard Forms. Check this computer's internet connection and try again.*

### Fill in and send a form

1. In the **Winlink forms** panel, pick a form. **Favorites** come first (Winlink Check-in and ICS213 General Message), then **All forms** by folder. Type in the **Find a form** box to search names and folders.
2. The form opens in its own window, titled *Winlink form:* and its name. It looks exactly as it does in Winlink Express. It is Winlink's own page, so it does not follow POTACAT's theme.
3. Fill it in and press the form's own **Submit** button. Most forms then show a box saying to click OK and close the window. Click **OK**; the window closes by itself.
4. The message is now in Winlink Mail's compose pane, with To and Subject filled in by the form. Press **Put in Outbox**. It goes out on the next **Send / Receive**, like any message.

A note above the text names the form and says Pat adds the form's data as an attachment. Some forms, the check-in among them, do not allow the text to be changed: the note then says *This form's message may not be changed; fill the form in again to change it.* and the text is greyed. To, Cc and Subject can always be changed.

Two things differ from Winlink Express:

- **Small question boxes are answered for you.** Where a form asks a question in a small box (the check-in's *Message Subject:*, every *Click to Add Date/Time*), POTACAT takes the form's suggestion at once: the current date and time, and the subject the form builds. You can type over the date field, and change the subject in the compose pane.
- **Your location is the centre of your grid square.** A form that asks for your location is given the centre of the grid square in **Settings > Station**, never the computer's own location. That is only as exact as the grid: a 4-character grid can be about 100 km off, a 6-character one about 5 km. It goes out in the sent form, so type your exact position into the form when it matters. With no grid set, the fields start at 0.0000.

### A form you received

A message that carries a form has a **View form** button above it. It opens the form as the sender filled it in, in a window titled *Received form:* and its name. If the forms are not on this computer yet, POTACAT says so; the form's text is still in the message itself.

Some forms name a reply form; the ICS-213 does. On such a message in the Inbox or the Archive, a **Reply with form** button appears. It opens the reply form already filled in with the original's details. Submit it, and it comes back to the compose pane addressed to the sender.

### Links and safety

If a form tries to open a web page (the check-in links what3words, for example), POTACAT asks *This form wants to open a web page.* with **Open in my browser** and **Cancel**. The page opens in your own browser, never inside POTACAT.

A form is a web page written by someone else, and a received form came from whoever sent it. POTACAT shows it in a closed window: it cannot reach the internet, your files, or the parts of Pat that connect, send or delete mail, and it cannot use your camera or microphone.

Forms need Pat 1.0.1 or newer, which POTACAT's own Pat is. With an older Pat set under **Settings > Station > Winlink > Advanced**, the Forms panel says *Winlink forms need Pat 1.0.1 or newer.* and names the version it found.

## Favorites, Templates and the Address Book

From 1.14.4, in the Winlink Mail window on the desktop. These are not in ECHOCAT Web.

- **Favorite gateways.** The star beside the gateway list saves the gateway you picked. Favorites keep their place in the propagation order, marked with a star, and one missing from the list shows at the end. A call to a favorite or a [History](#history) gateway uses the bandwidth that gateway offers (2000 Hz on ARDOP), not 500 Hz. The radio's dial shows in the top bar, with **Retune** when it is off the gateway.
- **Templates.** **Templates** lists Position report, POTA spot and your own. **+ Add new template** makes one, and **Save as template** saves the message you are writing.
- **Address book.** To and Cc suggest saved contacts, groups and people from your mail as you type. The book button beside To opens the **Address book**, which holds contacts and groups. A message from someone not saved has **Add to address book**.

## Sending and Receiving

Messages you write wait in the **Outbox** until the next **Send / Receive**. Choose how they go in **Send via**.

> **Where Winlink works, as of 1.14.6.** Internet mail works on Windows, Linux and Mac. ARDOP and packet over the radio are built in on all three; packet mail has gone through on the air, and on the Mac neither has been confirmed with a gateway yet. VARA HF and VARA FM are your own copy of VARA.

### Over the internet

Pick **Internet (telnet)** in **Send via** and click **Send / Receive**. This works on Windows, Linux and Mac, and never uses the radio.

If you want mail fetched without asking, set **Check mail over the internet every … minutes** in Settings. That check uses the internet only, never the radio. A radio session always starts from your own **Send / Receive**.

### Over the radio with ARDOP

1. Pick **ARDOP (radio)** in **Send via**.
2. Choose a **Band**, then pick a gateway from the list. The list is sorted nearest first. From 1.14.3 it keeps to the bands you set for your radio in [My Rigs](my-rigs.md), and says how many gateways it left out.
3. The radio tunes to the gateway straight away, and a waterfall with a **Busy** / **Clear** badge shows whether someone is already using the frequency.
4. When it reads **Clear**, click **Send / Receive**.

POTACAT handles the radio for the whole session:

- It moves the radio to data mode, keys it, and puts the dial back where it was. From 1.14.2 the radio stays put between attempts and goes back once, when you close the mail window or stop Winlink. The log says where it is going.
- From 1.14.2, an Icom stays in DATA mode for the whole session. Before, it was switched from USB to USB-D and back on every ARDOP frame.
- **Power**, **PWR** and **SWR** sit on the session line while you transmit.
- From 1.14.5, a **TX level** slider sits next to **Power**. It sets how loud the modem's audio goes into the radio's sound card for ARDOP and packet. It is modulation, not RF power. Until 1.14.5 that level was JTCAT's Drive slider; it starts at the level Winlink already used, and then the two are separate. On Flex Direct and Icom Network it is greyed out, because the radio's power sets the level there.
- From 1.14.5, the session summary shows the audio levels: what the modem heard from the radio, and what reached the radio at your TX level. When the audio reached full scale on a sound card, it says to turn **TX level** down to about 50% and watch the radio's ALC.
- From 1.14.6, the modem's input level shows next to **Busy** / **Clear**, for example *Input -18 dBFS*. At -3 dBFS or above it says *Input too high*: turn down the radio's USB or data audio, or the sound device's input, so the modem can hear when the channel is clear.
- From 1.14.6, when no radio audio reaches POTACAT, the waterfall says so and why, instead of staying black.
- From 1.14.6, a session keeps the radio in its data mode even when JTCAT's **Switch radio to DATA mode** box is off.
- The SWR guard stops a session that is transmitting into a bad match.
- A session ends after the time limit you set (**End a radio session after … minutes** in Settings). A stuck session also ends after 3 minutes with no progress, and the transmitter is released if it stays keyed for 30 seconds.

### Over the radio with VARA (Windows, your own copy)

> **New in POTACAT 1.13.2.**

> **Note:** From 1.14.4, VARA can also run on another computer, or under Wine on a Mac or Linux. **Settings > Station > Winlink > VARA (your own copy)** has a **Host** box: leave it blank for VARA on this computer, or type another computer's name or address, then press **Test** to see whether VARA answers. POTACAT never starts VARA there, and VARA on another computer uses that computer's sound card. Wine has not been tested.

VARA is EA5HVK's modem. You install and license it yourself; POTACAT doesn't install or download any part of it. Without a licence, VARA runs at reduced speed.

**What to install first:**

1. **VARA HF**, and **VARA FM** if you want VHF/UHF, from [rosmodem.wordpress.com](https://rosmodem.wordpress.com/).
2. **Only for a FlexRadio on Flex Direct or an Icom over the network:** two free virtual audio cables from [vb-audio.com/Cable](https://vb-audio.com/Cable/), **VB-CABLE** and the **Hi-Fi Cable** (or the donation A+B pack). Run each installer as administrator, then reboot. A radio with a USB sound card needs no cable; VARA uses the sound card directly.

**Then, in Settings > Station > Winlink (email over radio) > VARA (your own copy, Windows):**

1. Tick **Use VARA HF** or **Use VARA FM**.
2. Click **Set up VARA HF for me** (or **Set up VARA FM for me**). POTACAT configures VARA for the active radio, including its sound card or the cables, PTT (set to VOX) and the port. It then starts VARA and checks that VARA opened the devices. VARA is configured again whenever a session starts it or you switch radios.
3. Leave **Start VARA for me when a session needs it** ticked. VARA starts once and stays open between sessions; POTACAT never closes it.

VARA must never use POTACAT's own COM ports. If a VARA FM or VARA HF setting names POTACAT's CAT, PTT or CW key port, setup logs it, and POTACAT won't start that VARA until you change it (set VARA's PTT to VOX).

From 1.14.1, POTACAT leaves VARA's port settings alone, and no longer sets VARA FM's PTT option. 1.14.0 could write COM0 into VARA's PTT port, and VARA FM then stopped at start with a **port COM0 unable to open** dialog that blocked unattended connects from a phone or tablet. If you see that dialog, the log names the setting to fix in VARA FM.

If you run both, set VARA FM to port **8310** in VARA FM's own settings, because both programs ship on 8300.

**The gateway list:** from 1.14.3 every gateway list, VARA HF's included, loads at once, nearest first (propagation ranking needs your own VOACAP install for now). The log and the gateway line say when the ranking service isn't available. The list also leaves out gateways outside the bands set for your radio, and says how many. In 1.13.10 to 1.14.2 the list could take a long time to appear.

**Sending:** pick **VARA HF (radio, your own VARA)** or **VARA FM (VHF/UHF radio, your own VARA FM)** in **Send via**, choose a gateway, and click **Send / Receive**. POTACAT levels the audio both ways. The radio audio VARA hears is trimmed before it reaches the red, and VARA's transmit audio is raised to full scale, so the power you set is the power that goes out. The Mail window shows both levels during a session (**to modem … · from modem …**).

A session you stop stays stopped, and a new session waits for the last one to hang up.

### Also listed, not recommended yet

**Send via** also lists **Packet (VHF/UHF radio)**, which uses the Dire Wolf modem built into POTACAT. As of 1.14.5, packet mail has gone through on the air. On a Mac it has not yet been confirmed with a gateway.

From 1.14.4, Mercury is no longer offered for Winlink: no Winlink gateway runs Mercury. The Mercury HF Data chat window under **More** is unchanged.

Packet talks to Dire Wolf on its **AGW port, 8010**, on this computer. If another program already uses port 8010 (a Dire Wolf you started yourself, for example), close it first. From 1.13.10, starting Dire Wolf no longer closes POTACAT.

From 1.14.2, packet's **TX delay** and **tail** can be set in **Settings > Station > Winlink**, next to **Packet speed**. The defaults are 500 ms and 200 ms. The old fixed delay of 300 ms was too short for a radio keyed over CAT, so gateways missed the start of each frame. A packet session longer than five minutes is no longer cut off.

From 1.14.5, packet closes its link to the gateway cleanly. When a session ends, the modem stays up until the gateway answers the disconnect, 10 seconds at most, and the status bar shows **Closing the link to** the gateway meanwhile. Press **Stop** a second time to end it at once. Before 1.14.5 the gateway could keep the old link open and turn away every call for up to 15 minutes.

If a gateway answers a call but sends no greeting, the status says: *The gateway is still holding the last link, or its greeting did not decode here. Wait a few minutes and try again. If it keeps happening, check the receive level.* POTACAT does not retry such a call by itself.

## When a Session Does Not Finish

This section describes POTACAT 1.14.5. The plain sentences below arrived in 1.14.4; before that the Mail window showed a program error.

Radio links drop. On HF it is normal for some sessions to end part way, more so on a long or fading path. Mail you wrote stays in the **Outbox** until a gateway has taken it, and it goes on the next try.

The Mail window says what happened in a sentence, and for a radio session it shows a card with **Try again** (the same gateway) and **OK**. The phone and ECHOCAT Web show the same sentence.

### What the sentences mean

The gateway is shown here as KY4RY.

| The Mail window says | What it means | What to do |
|---|---|---|
| "KY4RY did not answer." | The gateway never replied to the call. | Try again, or try another gateway or another band. |
| "The call to KY4RY did not connect." | The call did not get through, and POTACAT cannot say why. | The same. |
| "The link to KY4RY dropped before the mail exchange finished." | The gateway answered and mail started to move, then the radio link was lost. POTACAT tries once more by itself (see below). | Let the automatic retry run, or press **Try again**. |
| "The link to KY4RY dropped again." then "POTACAT already tried once more by itself. Try another gateway or another band, or try again later." | The automatic retry dropped too. POTACAT does not try a third time. | Another gateway or band, or later. |
| "...nothing got through for 120 seconds, so the modem ended the link." | ARDOP only. The number is the ARDOP link timeout in force: 120 unless you changed it. | As for a drop. A closer gateway or another band often helps; a longer ARDOP link timeout helps on a fading signal. |
| "...KY4RY ended the link." | ARDOP only. The gateway hung up. | Try again. |
| "...KY4RY stopped answering." | ARDOP only. The gateway went quiet at the end and never confirmed. | Try again. |
| "The gateway is still holding the last link, or its greeting did not decode here." then "Wait a few minutes and try again. If it keeps happening, check the receive level." | Packet only. The gateway is still busy with an earlier link, or POTACAT could not hear its reply. | As it says. |
| "POTACAT stopped the session: nothing moved for 3 minutes." | Nothing at all happened for three minutes. | Try again, or try another gateway or another band. |
| "POTACAT stopped the session at its 30-minute limit." | Sessions have a time limit: 10 to 60 minutes, 30 unless you changed it. | Press **Send / Receive** again to carry on. |
| "POTACAT stopped transmitting: the SWR guard tripped." | The antenna match was too poor to transmit safely. | Check the antenna and its match, then try again. |
| "The radio did not transmit: ..." | The radio or POTACAT refused to key, for the reason given. | Put that right, then try again. |
| "POTACAT stopped the session: the transmitter stayed keyed for 30 seconds, so POTACAT unkeyed it." | The transmit failsafe acted. | Check that the radio has gone back to receive, then try again. |
| "The radio's sound device stopped: ..." | The radio's audio device went away. | Check the radio's USB cable and its sound device in **Settings > Radio**, then try again. |
| "The internet connection to Winlink closed before the mail exchange finished." or "Could not reach Winlink over the internet." | Internet sessions. | Check this computer's internet connection, then try again. |
| "You stopped the session." | You pressed **Abort** (or **Stop** on a phone). | Nothing. |

A few rarer endings are each followed by "Try again. If it happens again, send a Report a Bug.": "POTACAT's modem audio stopped, so the session could not go on.", "The modem (ardopcf) stopped during the session." and "The modem (ardopcf) closed its audio connection to POTACAT, and the link to KY4RY ended before the mail exchange finished." The modem's name follows the mode. A refused password says "Winlink refused the password. Check it in Settings > Station > Winlink."

### What got through

The line after the first sentence says what moved, for example "So far: 1 sent, 0 received." and "2 messages are still in your Outbox and will go on the next try." When everything went, it says "Your Outbox is empty: everything you wrote was sent." POTACAT only says what it could read back from the mailbox. If it could not read a number, it leaves it out.

### One automatic retry

When a radio link connected and then dropped before the mail exchange finished, POTACAT tries once more by itself:

1. It waits 20 seconds. The Mail window shows "Trying KY4RY again in 20 s." with **Try now** and **Cancel**.
2. It checks that nothing is transmitting and that the channel has been clear for 10 seconds. If the channel is busy it shows "Waiting for the channel to clear before trying KY4RY again", for up to another minute. If it gives up, it says so, for example "Not retried: the channel stayed busy."
3. It calls the same gateway on the same frequency, once.

It never retries after "did not answer", "did not connect", a gateway still holding the last link, Abort, the SWR guard, the time limit or any of the rarer endings, and never for an internet session or a Guest Pass session. The **Try again** button is still there.

To turn it off, untick **Try again once by itself when a link drops** in **Settings > Station > Winlink**. It is on by default.

### ARDOP link timeout

**ARDOP link timeout** in **Settings > Station > Winlink** is how long the modem keeps trying when nothing is getting through before it ends the link: 90 to 180 seconds, 120 by default. A longer time helps when the signal fades in and out. The gateway has its own limit and may still hang up first.

### History

**History** in the Mail window shows the last result for each gateway in the same words, among them "Mail exchanged (1 sent, 2 received)", "Link dropped before the mail exchange finished", "Connected, but the mail exchange did not finish" (a session you stopped), "Did not answer", "Did not connect", "Winlink refused the password", "Stopped", "Stopped: the channel was busy" and "The modem was not running".

### If it keeps happening

If sessions to gateways that used to work now drop often, use [Report a Bug](../community--support.md#report-a-bug) right after one. The report carries a one-line summary of each recent Winlink session (gateway, frequency, how long it ran, what moved, which side ended the link) and the modem's own log for the last three sessions, so there is nothing else to collect.

## Audio for Radio Sessions

- **FlexRadio on Flex Direct, or an Icom over the network:** ARDOP needs no sound card and no DAX. VARA needs the two virtual audio cables described above.

Radio sessions need a radio with CAT control, because POTACAT tunes and keys it.

From 1.13.2, ARDOP and packet take their audio over POTACAT's own link to the radio on every system, so there are no sound devices to pick by hand. VARA has its own audio setup (see [above](#over-the-radio-with-vara-windows-your-own-copy)).

## Troubleshooting Radio Sessions

These were fixed in 1.14.3. If you see one of them, update first.

- **ARDOP: the gateway never answers.** Most ARDOP frames went out with their start cut off, so gateways couldn't hear the connect request. POTACAT now sends that first audio at key-down.
- **The channel is busy.** The prompt offers **Keep waiting**, **Call anyway** and **Give up**. **Keep waiting** stays chosen and the prompt shows how long it has waited. **Give up** ends the wait cleanly. Use **Call anyway** only when you have listened and the frequency is clear. A session waiting for a clear channel is no longer ended as stalled.
- **Packet on an Icom loses the start of each frame.** On an IC-7100 through rigctld, the radio was switched to FM data before every over and keyed late. It is now set once per session, before the first frame.
- **VARA FM on VOX is refused.** A VARA FM set to VOX was refused when its settings still named POTACAT's radio port from an earlier choice. It now starts.

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

The ECHOCAT app and ECHOCAT Web both have a **Mail** tab with a composer, gateway list, waterfall and **Send / Receive**. The app's folders are In, Out, Sent and Archive; it can show archived mail but has no Archive button, no Deleted folder and no Cc field. From 1.14.5, ECHOCAT Web's Mail tab has Archive, Deleted, Restore, Reply all, a Cc field and the sent line. The ECHOCAT app does not have them yet; an older app's Delete moves the message to Deleted, where it can be restored. The shack PC holds the mailbox and keys the radio, so the desktop must be on POTACAT 1.13.1 or later. Winlink is for the station owner only: the shack refuses mail from a Guest Pass. A VARA session started from the phone shows "Starting VARA HF on the shack PC" while VARA comes up, and a failure says what is wrong on the shack PC. See [ECHOCAT](../echocat.md).

> **Note:** A desktop that is [driving a remote shack](remote-desktop.md) can't start a radio session. Start radio sessions on the shack PC.

## Privacy

What POTACAT stores and sends for Winlink is described at [potacat.com/privacy-terms.html#winlink](https://potacat.com/privacy-terms.html#winlink).
