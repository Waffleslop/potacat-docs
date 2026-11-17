# Release Highlights

This page summarizes major POTACAT and ECHOCAT releases — it is not an exhaustive list of every patch.

### v1.14.6 "Jensen's Fourth Affair - Ham Radio" — November 2026

POTACAT runs a Zeus or Thetis SDR over TCI with no sound card, FreeDV digital voice receive is fixed on Windows and arrives on Mac and Linux, Guest Pass owners get Take the radio, Give it back and Cancel pass, and every contact records the rig it was logged on.

- **Zeus and Thetis over TCI.** A new kind of rig, "Zeus or Thetis (TCI server)": tuning, receive audio with no sound card, and the band scope from the server's IQ. On Zeus, JTCAT's digital modes and ECHOCAT voice transmit; the PTT button, voice macros, CW, Tune, SSTV and the ATU do not key a TCI rig yet. Thetis is receive only for now. Not yet tried on a radio. Thanks W5LEE. See [Zeus and Thetis (TCI)](nested/zeus-thetis-tci.md).
- **FreeDV digital voice (receive).** RADE V1 no longer closes POTACAT on Windows, and the speech plays whole and at the right speed (thanks W3MDT). New on Mac and Linux: FreeDV (700D, 700E, 700C, 1600) and RADE V1 decode there. ECHOCAT and ECHOCAT Web hear the decoded speech. PTT is off in FreeDV modes; FT8, SSTV, Winlink and Tune still key. See [FreeDV / PSKReporter](nested/freedv--pskreporter.md#freedv-digital-voice-receive).
- **Guest Pass:** the Share Your Rig window has Take the radio (Now or In 5 minutes, with an optional message), Give it back and Cancel pass (thanks NA4DQ). After 5 quiet minutes the guest is told the radio is free and may take it; nothing switches by itself. A guest is told in plain words where they stand, can use the station's own SDRs but not add one, and never receives the owner's SDR passwords or full settings. A guest's contacts reach the guest's own logger. See [Share Your Rig](echocat.md#share-your-rig).
- **Logging:** every contact stores its rig in ADIF MY_RIG, with a Rig column in the Logbook; ECHOCAT contacts are marked, with a Source column (thanks W5LEE); the DXCC number is in every record; the right country for KL7, KH8 and prefixed portable calls; JS8 and JTTY show by name; Logger32 keeps the date (thanks I3FIY); a TQSL program field with Browse, and a Flatpak TQSL is found on Linux; QRZ Logbook says whether each upload went; Sync Now on a second computer pulls the whole history.
- **Yaesu:** FTX-1 and FT-710 CW messages end cleanly (thanks W2XYZ and DA2PK); transmit audio over the network on an SCU-LAN10, tested on an FT-710 by DA2PK, Winlink excepted; the PWR meter shows forward power on the FT-710, FTDX10 and FTDX101; a long list of fixes from the CAT manuals for the FT-891, FT-991/991A, FTDX10, FTDX101, FTX-1 and FTDX5000 (thanks I3FIY); FT-991/991A split; a setup note to set the FT-891's DATA BFO to USB; a Yaesu on rigctld reads its power.
- **Kenwood, Elecraft and Icom:** "Transmit audio input" chooses the rear or front socket on the TS-480, TS-590S/SG, TS-890S and TS-990S, which fixes a TS-480 that sent no audio in 1.14.5; the ATU tunes on the TS-590S/SG (thanks VA2PSL) and on the Elecraft K3, KX2 and KX3 (thanks KH7QO); the Icom voice hint names each radio's own menu, and the IC-7610 note explains unlinking the CI-V USB Port (thanks KQ4UUR).
- **For each rig:** an amplifier drive limit POTACAT never goes above; no Power Off button for a radio POTACAT cannot switch back on; PTT on RTS with RTS/CTS flow control is caught (thanks W5PLC); SSB-over-DATA leaves FM and AM alone (thanks KS9B); a band-scope SDR can sit on the radio's IF output. See [My Rigs](nested/my-rigs.md).
- **CW:** the VFO window's PTT no longer sticks on "ON AIR" after a CW text macro (thanks DA2PK); the ECHOCAT Web paddle keeps better time (thanks LZ3AW).
- **Where Winlink works today.** Internet mail works on Windows, Linux and Mac. ARDOP and packet over the radio are built in on all three; on the Mac neither has been confirmed with a gateway yet.
- **Winlink:** the window shows the modem's input level next to Busy/Clear and says "Input too high" when the radio's audio is too loud; a black waterfall says why (thanks N5XHI); sessions keep the radio's data mode; packet on an FT-817, FT-857 or FT-897 through flrig puts the radio in PKT (thanks N5XHI); on a Flex the panadapter centres on the Winlink channel; the dial stays on the gateway while your phone's Mail tab is open.
- **FT8 / JTCAT:** Band Activity has a Stream and Stations switch, with Need and Park columns; clicking a second caller mid-QSO drops the first QSO instead of logging it.
- **Spots, ECHOCAT and more:** one Max Spot Age everywhere; the band filter follows your rig; a remote PC mutes the shack's audio while it transmits; Space as the talk key no longer toggles scan; screen readers name the rig on every control in the rig list; Directory arrow keys move from the row you clicked; SSTV's Open folder makes the folder; a Launcher start no longer makes the next start report a crash.

### v1.14.5 "The FAA Can't Ground WinLink Release" — November 2026

Winlink Mail gets Archive, a Deleted folder you can restore from, and Reply all, and every sent message says how it went out. Packet closes its link cleanly, Winlink gets its own TX level, and a Mac says plainly when macOS is keeping POTACAT from hearing the radio.

- **Where Winlink works today.** Internet mail works on Windows, Linux and Mac. ARDOP and packet over the radio are built in on all three; packet mail has gone through on the air (thanks NA4DQ), and on the Mac neither has been confirmed with a gateway yet. See [Winlink Email](nested/winlink.md).
- **Winlink mail:** Archive; a Deleted folder with Restore and Delete for good, emptied after 7, 30 or 90 days, or Never; Reply all; and a line on each sent message saying when and how it went out. ECHOCAT Web's Mail tab has the same actions; the ECHOCAT app does not yet. Thanks NJ2DX.
- **Packet closes its link cleanly**, so the gateway no longer turns away calls for up to 15 minutes, and a gateway still holding the last link is not called again. Thanks NA4DQ and N5XHI.
- **Winlink has its own TX level** slider next to Power (modulation, not RF power), and the session summary shows the audio levels.
- **Mac microphone access.** POTACAT says when macOS will not let it hear the radio, and where to fix it. See [Installation Issues](nested/installation-issues.md#microphone-permission).
- **WSJT-X Mode is impossible to miss.** An amber WSJT-X Mode chip leads the top bar, CAT shows "off", and one click turns the mode off. The setting has one name everywhere: Settings > Spots, "WSJT-X Mode". See [WSJT-X](nested/wsjt-x.md).
- **Guest Pass:** a valid pass is never shown as cancelled, and a pass that cannot be used says why in a sentence.
- **Activations:** a new callsign clears the other station's park, the park-to-park field takes six parks, QSOs from the log window and ECHOCAT join the activation, and a corrected park reaches POTA.app. See [Logging Contacts](nested/logging-contacts.md).
- **Logging:** no guessed 100 W; Import Log adds confirmations to QSOs you already have; "Download all confirmations again"; the DXCC Tracker says worked on an ADIF log; KG4 calls with a one- or three-letter suffix are United States.
- **FT8 / JTCAT:** changing mode stops transmitting and starts clean; your own transmissions show their offset; replies to a hashed call go out (thanks VK4KTW); the WSPR beacon no longer sends frames back to back, keeps your power, and reports the power it runs at (thanks NA4DQ).
- **Radios:** a Flex LSB slice hears the lower sideband; the FT8 view on a Flex lines up with the pan; the band scope keeps running for every device; power on the radio's real scale over network Kenwood CAT (thanks W5LEE); the FTX-1 shows Power Off only; data-mode audio settings named for six radios; a TS-480 sends FT8 with data send; custom CAT sliders stay where you drag them; a KiwiSDR on HTTPS connects.
- **CW:** the radio no longer keys itself after a remote session ends, and CW from ECHOCAT no longer drops the Xiegu X5105's CAT link (thanks N6UGP); the stuck-transmit check covers the whole message; {op_firstname} names the station you are sending to.
- **SSTV:** sending a picture from your phone no longer closes POTACAT (thanks NA4DQ); the radio is on the SSTV frequency before the picture keys; the frequency box takes what you type.
- **More fixes:** switching operator keeps each profile's own settings; the rig list survives a settings file POTACAT could not read; startup says why it did not connect to the radio; a net reminder names its net.

### v1.14.4 "The Ionosphere Appreciation Day Release" — November 2026

Winlink is steadier and easier to diagnose, the Elecraft K4 and Kenwood TS-890S get band scopes, the FT-710 band scope works on a Mac, and POTACAT and ECHOCAT share the same six themes.

- **Winlink:** a dropped link says what happened (thanks AE5JE) and is tried once more by itself; the ARDOP link timeout can be set, 120 seconds by default; Connect works after Abort; Report a Bug carries the modem's side (thanks NA4DQ); packet mode on the radio can be set per rig (thanks N5XHI and NA4DQ); VARA can run on another computer or under Wine; Mercury is no longer offered for Winlink.
- **Winlink Mail:** favourite gateways and History (thanks NJ2DX), Templates, an address book, and Position report and POTA spot as forms.
- **ECHOCAT Web's Mail tab** is made for a phone, and puts the radio back when you leave it.
- **FT8 / JTCAT:** every park of a two-fer is logged, an option re-spots the activator after a hunted contact, and QSO logged is a card. Thanks to ituri (DA2PK) on GitHub.
- **Band scope and radios:** Elecraft K4 panadapter; Kenwood TS-890S band scope; FT-710 band scope on a Mac; the FTX-1 hears GMRS; a KX3 with the 2 m module tunes 144.2 MHz; FTX-1 CW text plays.
- **VFO and frequencies:** frequencies read the VFO way (14.074.00 MHz); band buttons and typed frequencies pick the sideband; the Small VFO can use two lines; Small and Large keep their own places; Power On and Power Off show in the VFO window.
- **Six themes, the same as ECHOCAT:** POTACAT Light, She's On Frequency, POTACAT Dark, Midnight, Acid Burn and Miami Nights. Choose them in Settings > Display.
- **Logging and POTA:** Tab after the RST jump no longer skips a field; an activation keeps its grid; the QRZ state fill names the contacts left.
- **Privacy:** Report a Bug masks addresses, and no tokens or Guest Pass codes are written to the log.
- **Linux and Mac:** Tailscale on a Mac is found more reliably; the Small VFO clears the Mac window buttons; start at login works with a Linux distribution's package (thanks mdeltito).

### v1.14.3 "The Spiced Apple Cider Release" — November 2026

The VFO window comes in two sizes, Directory gets Favorites and the CB channels, and ARDOP and packet Winlink connect far more reliably.

- **A Large VFO and a Small VFO.** The button beside the gear switches between the full window and a one-line Small VFO, and VFO settings has one list per size for what each shows. See [VFO Window](nested/vfo-window.md).
- **Pick your CAT buttons** in VFO settings: NB, NR, ANF, APF, Preamp, Att, COMP, VOX, MON, RIT, Split, ATU, whichever your radio supports.
- **Directory Favorites.** Star a Landmark or a Channel and it appears under Favorites in Directory, in the VFO window and on the band scope. See [Directory](nested/directory.md#favorites).
- **The 40 CB channels** are in Directory > Channels, and **a channel can recall the radio's own memory**, offset and tone included, over Icom CI-V or rigctld.
- **Tune from your phone through the SDR** when POTACAT can't move the radio.
- **Winlink:** ARDOP frames keep their leader, a busy channel can be waited out or stopped, packet on an Icom sets FM data once per session, the gateway list loads at once and keeps to your bands, and VARA FM on VOX starts. Thanks deadeye007, NA4DQ, stroopeffect and N5XHI. See [Winlink Email](nested/winlink.md#troubleshooting-radio-sessions).
- **SSTV text styles:** a typeface, outline, shadow and letter spacing for each text line. SSTV also leaves a VHF/UHF-only radio where it is. See [SSTV](nested/sstv.md#text-styles).
- **Stop an event banner that runs all year** from the event's badge on the banner. See [The event banner](nested/dx-expedition-tracking.md#the-event-banner).
- **CW text over FLRig no longer closes POTACAT.** Thanks djrev_11688.
- **A remote shack's spots stop flickering**, and HOLD TO TALK stays on screen with a long shack name. Thanks electricfalcon and deadeye007.
- **FT-710 band scope** starts when the radio is powered on after the scope was opened. Thanks ride1226.

### v1.14.2 "The Osage Orange Release" — November 2026

Packet and ARDOP Winlink behave on more radios, FT8 can decode from a WebSDR, and a forgotten activation ends by itself.

- **A Cloud address per shack**, up to 3 per membership, so ECHOCAT can switch between shacks over Cloud. Name the shack in Settings > Cloud.
- **FT8 from a WebSDR.** JTCAT has a Receive audio choice: Radio (sound card) or WebSDR. JTCAT won't transmit while the WebSDR is the receive source. Thanks LZ3AW.
- **Custom CAT toggles show the radio's real state**, with a Read command and an ON when rule for each toggle. Thanks LZ3AW.
- **Power On and Power Off from a remote POTACAT**, in the CAT chip's popover.
- **Prior contacts.** Right-click a spot or an FT8 decode to see how often you have worked the station, when, and on which bands and modes. It reads only your own log.
- **A forgotten activation ends by itself** at the UTC day change or after 6 hours with no contacts, whichever comes first.
- **TX power in the VFO window**, and the mouse wheel now tunes up when scrolled up. See [VFO Window](nested/vfo-window.md).
- **Winlink:** an Icom stays in DATA mode for the whole session, the radio stays put between attempts, packet keys again on a rigctld rig, and packet's TX delay and tail are settable in Settings > Station > Winlink. Thanks NA4DQ and N5XHI.
- **Icom IC-7300 MK II over Icom Network:** set DATA MOD to LAN. Station Setup now says so, with the menu path. Thanks KJ5CHK.
- **A refused transmission plays no audio.** Thanks VK4KTW.
- **A hunter contact with a POTA and SOTA activator uploads the SOTA chase.** Thanks WV8T.
- **ECHOCAT Web: HALT is never hidden**, and Tailscale on a Mac shows its real state.

### v1.14.1 "The Saturday Sweep" — November 2026

Eleven fixes from the first week of the public bug tracker, and WSJT-X's "Fake It" split for JTCAT.

- **Split operation "Fake It"** keeps your FT8, FT4 or FT2 tone in the middle of the radio's filter. See [Fake It](nested/jtcat.md#keep-your-tone-in-the-radios-filter-split-fake-it).
- **A Yaesu left keyed after a CW message is unkeyed.** POTACAT checks up to three times that the radio has dropped out of transmit after a CW message from ECHOCAT or the desktop.
- **Xiegu G90 through rigctld:** the radio is left alone while it unkeys, so the bundled rigctld no longer crashes during FT8.
- **RTS line: "Asserted, no flow control"**, for a CAT cable through a box such as an LDG YT-1200's PC port. A serial port stuck waiting for CTS can now be closed. See [The RTS line setting](nested/cat-control-issues.md#the-rts-line-setting).
- **The FT-710 band scope restarts itself** when it stalls or the radio comes back; nothing is restarted while you transmit.
- **SCU-LAN10 scope on the FTDX10 (experimental)** now draws instead of staying blank. Thanks VK4KTW.
- **VARA FM's port settings are left alone**, so VARA no longer stops on a "port COM0 unable to open" dialog. Thanks N5XHI. See [Winlink Email](nested/winlink.md#over-the-radio-with-vara-windows-your-own-copy).
- **A "Log as" contact goes to that operator's Club Log and Wavelog accounts**, and Club Log uploads go through an outbox.
- **Guest Pass contacts no longer wait until a restart** to be sent.
- **WebSDR:** a spot click no longer brings seconds of noise.
- **Check for Updates always says what it found.** It's the link at the bottom of Settings, or press F5.

### v1.14.0 "The Neptune square Mars, Neptune square Venus Release" — November 2026

Hunt gets filters: answer several targets at once, choose who goes first, never answer a station you name, and see in one line why Hunt is quiet. POTACAT now unkeys any transmission that runs too long, a Yaesu no longer keys up as POTACAT opens its port, and a spot click no longer changes your filter width. Yaesu's SCU-LAN10 network adapter arrives as an experimental radio type.

- **Hunt filters**, in the FT8 window and ECHOCAT Web: **Hunt: Custom** answers several targets at once, **Hunt: New grids**, **Who goes first** (Strongest, Farthest, Needed first), **Never answer** (a call or a prefix like VE3*), a 30-minute skip after a QSO gives up, and **Hide decodes below N dB**. A line under Hunt says why it's quiet. Hunt no longer answers a CQ DX from your own continent. See [Hunt filters](nested/jtcat.md#hunt-filters).
- **A time limit on every transmission POTACAT starts**, from 30 s for FT8 to 10 min for voice. See [Transmit Time Limits](radio-setup.md#transmit-time-limits).
- **A Yaesu no longer keys up as POTACAT opens its port.** A radio whose CAT RTS menu is on is tried with RTS/CTS after 6 s. Thanks G5HOW. See [Yaesu: keys up on connect](nested/cat-control-issues.md#yaesu-keys-up-on-connect-or-doesnt-answer).
- **A spot click keeps your filter width.** See [Filter Width](radio-setup.md#filter-width).
- **Yaesu SCU-LAN10 (experimental):** CAT, receive audio and the band scope over the network for the FTDX10, FT-710 and FTDX101D/MP. No transmit audio over the LAN yet. See [Yaesu SCU-LAN10](nested/yaesu-scu-lan10.md).
- **Icom radios that drop replies are sent one command at a time** (Advanced > CI-V pacing). Thanks NA4DQ. See [CI-V pacing](nested/rig-ic-7300.md#ci-v-pacing-mode-or-power-never-reported).
- **Full power (W)** in Settings > My Rigs, for a radio POTACAT reads as the wrong size, such as a 5 W Hermes Lite shown as a 100 W TS-2000. Thanks W5LEE. See [Full Power (W)](nested/my-rigs.md#full-power-w).
- **Guest Pass:** a guest is told why a transmission was refused, and the owner what to fix. Thanks KF0WWL.
- **Kenwood:** a Kenwood behind rigctld keeps its power at connect; a silent Kenwood is tried with RTS/CTS; the TS-890S is a 100 W radio.
- **SSB over DATA** keys once the radio reports the DATA mode and sets the mode and frequency first, so overs aren't clipped or off frequency (GitHub #113).
- **The external tuner's tune never sets 100 W** (GitHub #111). The first tune after connecting no longer cancels a split (GitHub #113).
- **"The audio interface keys it" on FLRig and rigctld Network**, for a TS-2000 with a SignaLink and similar. Thanks WX4MWA. See [Transmit (PTT)](radio-setup.md#transmit-ptt-how-the-radio-is-keyed).
- **rigctld restarts itself** when it stops. Thanks LA8JKA. Custom CAT buttons over Hamlib can send rigctld's own commands (`+V VFOB`).
- **Voice at 0 W names the radio menu that's missing the audio**, and **Station Setup checks voice transmit**; its test transmit moves to a frequency your licence allows. Thanks KD9OUT, KD9WJY and KJ5CHK. See [Voice is silent, but FT8 works](nested/ssb-over-data.md#voice-is-silent-but-ft8-works).
- **FT8, FT4 and FT2 spots tune the dial** (7074, not the 7075 the spot names); FT4 replies can start up to 2.5 s into the slot; 2 m WSPR tunes 144.489.
- **SSTV:** Robot 36, Scottie, PD and Robot 72 pictures from MMSSTV decode. See [SSTV](nested/sstv.md#modes-and-mmsstv).
- **Logging:** N3FJP confirmations go to the right service and a daily re-read never removes one; eQSL and ClubLog count as confirmed; GridTracker logs and spots each contact once; the Activator log never loses or doubles a contact; a General contact never picks up the last park; QRZ's county is used only for US stations. Thanks K0DHW and IK4IDF.
- **Settings are written safely, with a backup.** Thanks N8JMS. To reset settings, delete both `settings.json` and `settings.json.bak`.
- **VARA never keeps POTACAT's COM ports.** Thanks N5XHI. See [Winlink Email](nested/winlink.md#over-the-radio-with-vara-windows-your-own-copy).
- **One Change Theme dropdown**, and the ECHOCAT app's waterfall colours on every desktop waterfall.
- Setup notes name the Silicon Labs CP210x driver for the FT-991A, FT-891, FT-710 and FTDX10.

### ECHOCAT app updates — November 2026

Over-the-air updates to the ECHOCAT app (every 1.5.x version). They arrive by themselves when the app starts.

- **CW macros:** the phone's sidetone plays the same words the radio sends, and macro timing is even with sidetone on.
- **Wired earbuds:** a press of the earbud button keys PTT at once. See [Transmitting](echocat.md#transmitting-ptt).
- **SSTV:** the template browser has a **From desktop** section with your desktop's templates. See [SSTV](nested/sstv.md).
- **CW macros:** receive audio comes back sooner after a macro, about 0.25 s on your home network and under 0.5 s over Cloud.
- **Activator log:** a General contact never carries the previous park. Contacts already logged that way need the park removed by hand, and re-uploading if they were sent to POTA.

### v1.13.10 "The Wednesday Special" — November 2026

- **The FT8 window is rebuilt:** one button for band and mode, large action buttons (Call CQ, Hunt, HALT, Tune, ATU, Logbook, Options), and new Hunt targets: New countries, DX only, Same as Call and Watchlist. See [The FT8 Window](nested/jtcat.md#the-ft8-window).
- **Review a contact before it's logged:** FT8 window **Options** > **Open the Log QSO window before saving**. Thanks AE5JE. See [Review a contact](nested/jtcat.md#review-a-contact-before-its-saved).
- **"JTCAT FT8" in the comment** is now a setting in Settings > Logging.
- **FT8 on 2 m and up is no longer refused** by the license check, which now covers 2 m and higher, all of 60 m, the CW-only band edges and US Advanced.
- **Guest Pass** can operate the station and nothing else, and its power cap is set on the radio. See [Share Your Rig](echocat.md#share-your-rig).
- **ECHOCAT can be Cloud only or Off:** Settings > ECHOCAT > Who can reach this computer. See [Who can reach this computer](echocat.md#who-can-reach-this-computer).
- **One shack per Cloud address:** a second desktop asks before it takes the address. Thanks KQ5O.
- **DXLab Commander** is a radio type. See [DXLab Commander](nested/dxlab-commander.md).
- **PTT on the CAT port's RTS or DTR line**, for radios such as the IC-706MKIIG. See [Transmit (PTT)](radio-setup.md#transmit-ptt-how-the-radio-is-keyed).
- **Test Connection names a port another program holds.** See [Sharing Your Radio with Other Programs](nested/sharing-your-radio.md).
- **The scope pop-out** works like SmartSDR: spot labels in the trace, click to tune, drag the frequency scale to resize.
- **Winlink:** the VARA HF gateway list gets two minutes; ARDOP no longer stops on a Mac; starting Dire Wolf no longer closes POTACAT.
- **Two new themes:** Miami Nights and She's On Frequency.

### v1.13.9 "El Día de los Bichos Muertos" — November 2026

A release of bug fixes, most of them reported by users. JTCAT stops logging contacts that never finished, Halt TX stops a transmission everywhere at once, and the band follows your radio when you turn the dial to another band's FT8 frequency.

- **FT8 / JTCAT:** no log for a contact that never finished; **Halt TX** stops the transmission on every screen, the phone included; the FT8 window follows the radio to another band's FT8, FT4 or FT2 frequency; new grid, new call and new DXCC badges clear once logged; a six-minute transmit limit when nothing progresses; DXpeditions that announced an FT8 or FT4 frequency appear in the band menu; the signal-floor boxes save; GridTracker keeps its map and roster.
- **Logging:** the country is where the station is operating (6W/IK2HKT is no longer logged as Italy); the Log QSO window, the log pop-out and ECHOCAT Web's log forms show the bands and modes you have already worked with a call; the Log QSO form follows your radio.
- **POTACAT refuses a transmission outside your license class**, using the License Class in Settings > Operator.
- **Radios:** Yaesu FT-710 CAT corrections from an owner; Kenwood TS-590S/SG and TS-890S filter width; Elecraft K3, K3S, KX2 and KX3 go into DATA A for FT8 and WSPR; Icom split and VFO B are read; Wideband FM on the IC-7100 and IC-705; a Xiegu G90 with a Digirig no longer transmits as POTACAT connects; TX power through Hamlib uses Hamlib's own scale; an external tuner gets its power back after a tune; a renumbered COM port can be picked; an FTX-1 can tune NOAA weather and marine channels.
- **Flex:** More > Tuner Memories fills the radio's own antenna tuner memories.
- **Maps and spots:** DXCC prefix labels (tick **Prefixes** in a map's legend, or press F9); FT8, FT4 and FT2 are separate mode filters again; the spot table no longer goes blank when a POTA fetch fails; park lists outside the US work.
- **Also:** paste a frequency into the VFO window; voice macros record properly; a Winlink error no longer closes POTACAT; `potacat` starts from a terminal on Linux.

### v1.13.8 "The Halloween Special" — October 2026

An RTL-SDR on your network becomes a second receiver, and the Directory gains Landmarks and Channels.

- **Listen through an RTL-SDR on your network** (rtl_tcp, or an SDRplay running rsp_tcp). The SDR takes over where your radio can't go, such as NOAA weather, and hands back when you tune where the radio can. The VFO window's volume knob sets the SDR's audio too, and the dongle is shared with the band scope. See [WebSDR, KiwiSDR and RTL-SDR Receive](nested/websdr.md).
- **Directory: Landmarks and Channels.** Landmarks are signals worth dialling into at any time, each explained. Channels is a frequency chart that is yours to edit: FRS, GMRS, MURS, marine and more.
- **Band scope:** on Flex Direct the FT8 window shows the radio's own waterfall; the Band Activity strip under the map is off by default again.
- **Radios:** KiwiSDR listening works on the new firmware; an Icom in DATA mode keeps its FT8 preset; a PTT port keys on RTS by default, as a Digirig needs.
- **Winlink:** radio sessions run on a "No CAT control" radio, such as an HT with a Digirig.
- **WSPR:** the beacon runs as long as you set; the 30-minute limit is gone.
- **Logging and activations:** N3FJP fills in the DXCC for US contacts; clicking a hunted activator at a two-fer fills every park; the activation toolbar wraps at large text sizes.
- **Installing:** upgrades no longer stop at "POTACAT cannot be closed".

### v1.13.7 "The Brits Put Beans on Toast Release" — October 2026

Modern Icoms show their own band scope live in POTACAT, on your phone and behind the spots. Yaesu CW macros send Morse again.

- **The Icom's own scope, live,** on an IC-7300, IC-7300 MK II, IC-705, IC-9700, IC-905, IC-7610, IC-7851 or IC-7760. An Icom with no scope over CI-V, such as the IC-7410, is told so.
- **Band Scope window:** frequency and level scales, a cursor readout, Top and Bottom levels, the passband, split TX frequency and band edges drawn on the scope, and tuning with the mouse. Bandspread draws the radio's scope as a faint trace behind the spots.
- **Yaesu CW macros send Morse, not a carrier,** on the FTX-1, FT-710 and other recent Yaesus.
- **Radios:** FTX-1 preamp steps (IPO, AMP1, AMP2); **Voice over the LAN stays in USB / LSB** for an Icom on Icom Network whose DATA OFF MOD is LAN; a receive level for your phone or browser; Flex Direct on a PC with no microphone starts the audio bridge.
- **WSPR:** on a radio connected through rigctld, the beacon's power cap no longer means full power.
- **Presets:** NB and DNR levels show the radio's real range, and a preset holds a preamp step.
- **Logging:** a contact is never logged without a mode; your grid goes to N3FJP and other loggers as MY_GRIDSQUARE; QLog logs that name the park only as POTA_REF import with the park.
- **Themes:** the ECHOCAT themes on the desktop, under Settings > Display > Theme.
- **Also:** CW on a Mac stays even when POTACAT is in the background; ECHOCAT Web's Cloud sign-in asks for email or callsign.

### v1.13.6 "Flex and Icom Bandscope and Rig Swap Improvements Release" — October 2026

On Flex Direct, POTACAT shows the radio's own panadapter as its band scope. Sharing your rig becomes a proper loan: a guest operates under their own callsign.

- **The Flex's own panadapter** in More > Band Scope, under the FT8 waterfall and on your phone, with readings in dBm. The FT-710's scope reaches the phone's Pan tab. Guests may zoom and centre the scope; your settings come back afterwards.
- **Share my Rig:** a guest signed in to POTACAT Cloud transmits under their own callsign; friends can take turns during a pass; the Guest Pass banner has **Take over** and **Give it back**; when a pass ends, every transmission stops and the guest is disconnected; guests bring their own voice macros, which are never stored.
- **Radios:** the Flex reports its real settings; rig presets set NB and NR levels in the radio's own steps; the SWR guard clears when a bad match is fixed outside POTACAT.
- **FT8 / JTCAT:** GridTracker as your call roster; **Hunt: don't call below** a signal level; Hunt honours Skip Grid.
- **Logging:** your own state and county on every contact (Home state and Home county in Settings > Station); a park in several states takes the activator's state from their spot; a reminder when your log is not backed up to POTACAT Cloud.
- **ECHOCAT and the VFO window:** the VFO window's profiles sit in a drop-down under the dial; a voice macro renamed or recorded elsewhere shows straight away.
- **Also:** the SFI, K and A numbers have left the top bar for the Conditions window; a theme change reaches the VFO, Log, pairing and Band Scope windows; the Winlink recovery email can be seen and changed in Settings.

### v1.13.5 "The Monday Peanutbutter Sandwich Release" — October 2026

POTACAT decides what counts as DX the way you do: another country by default, or farther than a distance you set, with a DX tag and a "DX only" filter on the spot list.

- **What counts as DX.** A station in a different country (DXCC entity) from yours is DX, with no setup. The DX Cluster source is now labelled **Cluster**.
- **The SWL/HF Net Directory is always on,** with no setting, and phones on ECHOCAT receive it.
- **External tuners get a real carrier** with External ATU type set to **LDG / MFJ (RF-sense auto-tuner)**.
- **Power On and Power Off** in a Radio row at the bottom of the VFO window.
- **Radios:** a Yaesu tuned on VFO B stays on VFO B; Icoms on direct CI-V show forward power while transmitting; **Transmit (PTT)** in the Serial CAT rig editor for a radio keyed by its audio interface; FT-450 Test Connection no longer reports a false failure.
- **Audio devices are found again by name** when Windows or macOS gives the radio's sound card a new ID. Bug reports say whether settings are being saved.
- **FT8 / JTCAT:** the WSPR beacon's first slot transmits; the FT8 decoder is no longer restarted while there is no audio; the JTCAT map pop-out draws the QSO arcs.
- **Activations:** a park-to-park with a 2-fer: type the other activator's parks into the park box.
- **Windows:** no window can be shrunk past its own controls; the Conditions window remembers its size and position; the Worked All States table scrolls. Thanks N0KAH.

### v1.13.4 "The Shared Radio Release" — October 2026

POTACAT can share a radio with your logger or fldigi through flrig. Radios whose data port is silent in USB and LSB, such as the Xiegu G90, can carry voice over ECHOCAT. Contacts logged in N3FJP on its own can come into your POTACAT log.

- **New connection type: FLRig (a shared radio)** in Settings > My Rigs. Tuning, mode, PTT, meters, RF power, VFO A/B, split and the tuner start work through flrig; filter width, the noise blanker, CW keying over the CAT port and Custom CAT commands stay in flrig. Thanks KM4CFT.
- **Voice in DATA mode (USB-D / LSB-D)**, a checkbox in the rig editor, for the Xiegu G90 and radios like it. Contacts are still logged as SSB.
- **Radios:** the Xiegu G90 is set up through Hamlib when picked as the Radio Model; a rigctld server that cannot key the radio is named in the log and in a notice; Linux `/dev/serial/by-id` ports are no longer reported as missing.
- **Bring in contacts from N3FJP:** Settings > Logging > Send Data to Logbook.
- **Activation panel:** a frequency typed in kHz into the MHz box, such as 7182, is read as MHz.
- **ECHOCAT:** a voice macro recorded on the phone is confirmed by the shack, and every connected device sees it.

### v1.13.3 "The Right Band, Right Slot Release" — October 2026

- **Each radio shows only its own bands**, everywhere in POTACAT; tick extra bands for a transverter or a 4 m export model. See [Your Radio's Bands](nested/my-rigs.md#your-radios-bands).
- **FT8, FT4 and FT2 slot lock:** **Slot** > **Auto**, **1st (even)** or **2nd (odd)**. See [JTCAT](nested/jtcat.md#making-qsos).
- **Spot yourself on POTA by Winlink** with **Spot by Winlink** or **POTA spot**. Thanks W7RTA. See [Winlink Email](nested/winlink.md#spot-yourself-on-pota-by-winlink).
- **Logging:** GridTracker now accepts POTACAT's QSOs; frequencies are read in MHz, kHz or Hz, and older contacts saved with MHz as kHz are repaired (with a backup kept); an FT8 contact with no CAT is logged on the FT8 dial.
- **Rig profiles** can set **Monitor (MON)** and **Monitor level**. Thanks K8IKO.
- **WSPR map legend** for its SNR colours.
- **Fixes:** a second VARA session in a row works; the gateway list error "invalid character ':'" is gone; a COM port Windows lists is never called missing; Yaesu voice macros stay in USB/LSB under SSB over DATA; ECHOCAT no longer restarts audio for a squelched FM or no-CAT radio.

### v1.13.2 — October 2026

- **Winlink with your own VARA HF and VARA FM** (Windows), set up in one click with **Set up VARA for me**. See [Winlink Email](nested/winlink.md#over-the-radio-with-vara-windows-your-own-copy).
- **ARDOP and packet on macOS**, using POTACAT's own audio link to the radio.
- **Worked All States**: worked and confirmed states and countries by band and mode, tinted on every map (F6 / F7 / F8), LoTW and QRZ fill-in, and **Hunt: Wanted states** in FT8. See [Worked All States](nested/worked-all-states.md).
- **Rig profiles**: Settings > Profiles can set TX power, gains, filter, NB, NR, notch, compressor, VOX, preamp, attenuator and AGC, by mode and by band. See [Rig Profiles](radio-setup.md#rig-profiles).
- **Guest Pass:** a guest can listen to any spot; transmit is checked against their license and the pass.
- **Radios:** Ten-Tec Jupiter and Argonaut V, Kenwood TS-2000 direct serial, a missing COM port is waited for, Yaesu FTM-510D and Icom IC-7410 in the picker, PTT on ECHOCAT Web for sound-card-keyed radios.
- **Sign in to Cloud with your callsign**, for Sign in with Apple / Hide My Email accounts.

### v1.13.1 — October 2026

- **Winlink email.** More ▾ > Winlink Mail sends and receives mail over the internet (Windows, Linux, Mac) and over the radio with ARDOP (Windows and Linux). Nothing to install. See [Winlink Email](nested/winlink.md).
- **N1MM+ (or another logger) can control the radio** through POTACAT as a TS-2000 over TCP, including a remote shack you are driving. See [Radio Setup](radio-setup.md#let-n1mm-or-another-logger-control-the-radio).
- **Sound-card PTT** for radios with no CAT (Digirig Lite, CM108/CM119). See [Radio Setup](radio-setup.md#sound-card-ptt-for-radios-with-no-cat).
- **Yaesu SWR** now reads the SWR meter instead of ALC; Yaesu and Icom SWR are scaled like Hamlib and WSJT-X.
- **ECHOCAT:** the radio's audio is never taken from the PC's microphone; one **Password-protect your rig** setting replaces the access token.
- **Spots and logging:** a dim checkmark for "worked today on another band/mode"; the Log QSO form drags by its title bar; Ctrl+L brings the tuned spot's park.
- **SSTV:** a **Keep** button saves a picture decoded from a weak signal to Received.
- FT-817/818, FT-857 and FT-897 now use Yaesu's own CAT; IC-9700 network audio fixes; FT-710 rig preset **Use current** reads RF and AF gain.

### v1.13.0 "The KM4ACK Ham Fam Jam Release" — October 2026

- **Run your shack from another POTACAT.** Pair a laptop with the shack PC and drive the radio: VFO window, HOLD TO TALK, FT8/FT4 and the other JTCAT modes, JS8, SSTV, CW, voice macros and the band scope. See [Run Your Shack from Another POTACAT](nested/remote-desktop.md).
- **More than one of your devices at a time** (beta, off by default) — phone and laptop can share the shack. See [ECHOCAT](echocat.md#more-than-one-of-your-devices-beta).
- **Rig presets** — named TX power / RF gain / AF gain sets, applied by a tap or automatically on a mode change. AF gain is a new rig control. See [Rig Presets](radio-setup.md#rig-profiles).
- **JTTY chats** — a tab per station in the JTCAT window, and CQ goes out on the clearest spot near your offset. See [JTCAT](nested/jtcat.md#jtty).
- **IC-7300 and family:** a spot click no longer leaves the radio in plain USB when the DATA frame is lost on a shared CAT port.
- Linux shacks on a tailnet can now be paired from away even when POTACAT can't run the `tailscale` command (snap installs).

### v1.9.4 — July 2026

- **13 Colonies** fixes across desktop and mobile, plus a 13 Colonies tracking list with notifications in the mobile `CNTSTS` tab.
- Connectivity bug fixes; the Tailscale certificate is no longer cached at startup (fixes Tailnet account changes).
- Matching mobile OTA updates — update both desktop and app.
- JTCAT fix for `RR73` decoded as a grid square; continued FT8 parity work with WSJT-X.
- iOS QR-scan fix for macro-lens iPhones; SSTV and Activator-mode updates on mobile.

### v1.9.2 + ECHOCAT mobile v1.1 — June 2026

- **Straight Key** on-screen CW button in the mobile app.
- Fully **customizable VFO screen** — hide and reorder elements.
- Improved pairing: one click to connect when paired with POTACAT v1.9.2.
- Up to **25 voice/CW macros**, synced across devices (older on-phone macros are wiped).
- Android landscape mode.

### ECHOCAT for Android — June 26, 2026

- ECHOCAT app live on **Google Play** (`co.cmox.echocat`) — $9.99 one-time purchase, includes all updates.
- Known bug at launch: connecting via "Discovered" was broken — use the QR scan instead.

### v1.8.16 — June 2026

- **Instant pairing** for Cloud subscribers: log in on any device and connect to your shack, over Tailscale or POTACAT Cloud off-LAN.
- **WSPR TX/RX** working; the **idle agent** can decode SSTV or WSPR (Settings > Station), with WSPR reports sent to PSKReporter.
- IC-7100 rig layer.

### v1.8.14 — June 2026

- **Late-start FT8 TX** — join a slot roughly 7 seconds late with a shortened reply (WSJT-X parity).
- **A-priori (AP) decoding** in JTCAT; day/night line added to the JTCAT map.
- **FT-710 ATU** control over CAT; per-rig audio settings under Settings > Radio.
- Remote **Stop Scan** from ECHOCAT; Linux arm64 build.

### v1.8.6 — June 10, 2026 — POTACAT Cloud launch

- **POTACAT Cloud** subscription: $5/mo or $50/yr with a free trial — cloud log backup, multi-device logging, parks-worked sync, and the **Cloud Tunnel** (`<callsign>.potacat.com`, no Tailscale required).
- **Cloud Sharing** stack: desktop-to-desktop pairing, **Share My Rig** links (start-now or scheduled, optional anonymous guests, 30-day guest link cap), and **tap-to-pair** on the LAN.
- Follow-ups in v1.8.7–v1.8.9: revoking access now kicks live sessions instantly, hardened cloud backup download, and a **TURN relay** for CGNAT (including double-CGNAT/Starlink).
- **Charcoal** dark theme (Settings > Display), Contests "What's Next" redesign, color-coded logbook columns with `Ctrl` `+`/`−` zoom.
- `STATION_CALLSIGN` now written on every QSO (LoTW / Part 97.119 attribution); **Flex per-band antenna mapping**.

### ECHOCAT for iOS — June 8, 2026

- ECHOCAT app live on the **App Store** — $9.99 one-time purchase, includes all updates.
- **ECHOCAT Web** continues to work and remains free; Tailscale remains an option.

### v1.6 — May 2026

- "Whole Lotta Things Working Well": initial **keyer support in the iOS/Android apps** — TinyMIDI, VBand, Vail, and HaliKey MIDI.
- **Flex Radio direct connection without SmartSDR** plus full **WinKeyer** support (May 21) — enables AetherSDR use with POTACAT.
- **POTACAT Cloud Tunnel** first working (June 2): connect a phone to the rig with no Tailscale — the foundation for rig swapping.

### v1.5.16 — May 2026

- Initial foundation for the **iOS and Android apps**; tester builds followed in the Hamvention build.
- **WebSDR + KiwiSDR** RX "finally working as intended" — listen on a remote SDR while transmitting on your own rig.
- FT8 timing and respot-logging fixes; ragchew logger pop-out with `Ctrl+F1`/`Alt+F1` hotkeys.

### v1.5.2 — April 2026

- "Mega GitHub Issue Squashing" release; POTA.app sync phase 1, with Cloud users auto-syncing POTA parks-worked.
- **Auto-SSTV RX on idle** (default on, 90-minute timeout); SSTV **Scottie S2** support.
- **CI-V over TCP**; IC-7200, TS-2000, and FTX-1 Optima rig profiles; CW keying hardening.
- ECHOCAT map pop-out to a browser window; iPad split-view support.
- **Logger32** added as a logbook forwarding target (April 25).

### v1.5.0 — April 2026 — "The SSTV Release"

- **SSTV** decoding: Martin M1 "on par with MMSSTV," with Scottie 1 close behind (first shipped in v1.4.8/1.4.9).
- **Mac, Linux, and Windows installers** built via GitHub Actions, downloadable at potacat.com.
- One-click **Report a Bug** (v1.5.1): redacted system snapshot, rig config, and log tail into a prefilled Discord post — grid square excluded.
- Milestone: roughly 6,000 downloads, 10,000 QSOs, and 102 versions in about 9 weeks.

### v1.4.x — April 2026

- **Desktop VFO dial with audio streaming on the PC**: knob, dialpad, mode selector, PTT, log button, operator heads-up display, and solar weather.
- **Multi-slice JTCAT for Flex** — monitor 4 or more slices at once.
- **WebSDR as an RX option** — SWL and HF-net listening, even for unlicensed users.
- **VFO Lock** and Elecraft K4/K4D rig profile (v1.4.2).

### v1.3.15 — April 2026

- **FreeDV on ECHOCAT** (bundled on Windows; Mac/Linux build the RADE decoder).
- **Voice Macros** — 5 slots, shared between phone and desktop, with auto-PTT.
- **Propagation Map** pop-out (RBN/PSKReporter, day/night overlay); GridTracker-style decode enrichment in JTCAT and ECHOCAT.
- ECHOCAT configurable, reorderable spot columns; TunerGenius 1x3 antenna switching.

### v1.3.11 — March 2026

- Native **ft8_lib decoder** replaces WASM — FT8 decoding 5–10x faster (~120 ms).
- Movable **S-Meter and SWR meter** on desktop and ECHOCAT.
- **K1EL WinKeyer (WK2/WK3)** keyer support and a floating, draggable **CW Macro** box with variables such as `{MYCALL}`, `{call}`, and `{op_firstname}`.
- **Keyboard CW** keying (VBand/Vail style: left `Ctrl` dit, right `Ctrl` dah, iambic timing).
- Activation **dupe detection** (DUPE tag and count badge); **Launcher** system tray icon on port `7301`.
- 10 Hz fine tuning on the ECHOCAT dial (v1.3.10).

### v1.2.2 — March 2026

- "Don't Cross the Streams": JTCAT FT8 decode fixed after crossed desktop audio streams.
- **MIDI remote CW** on ECHOCAT (Android only — iOS Safari blocks Web MIDI); local sidetone for CW macros.
- **Rig Model layer** decoupled from connection method, with unlimited **custom CAT commands** per rig.
- **Auto-chase** for POTA/SOTA/CQ spots; 4-row FT8 layout on ECHOCAT.

### v1.1.0 — March 2026 — "The FT8 + Remote CW Release"

- **Remote FT8** and **remote CW** on ECHOCAT; all CW/FT8 functionality rolled out free to everyone on March 19.
- **Watchlist band/mode filters** (v1.1.1): `K4SWL:20m`, `KI6NAZ:CW`, `W1AW:40m:SSB`.
- ECHOCAT **voice macros**, DTR keying for remote CW, and remote power on/off for Yaesu rigs.
- Electron 33→39 / Chromium 130→142 platform upgrade; docs.potacat.com link added in-app.

### v1.0.12 — March 2026

- **Rig Control Panel** (status-bar Rig button): ATU tune, noise blanker, power on/off, RF gain, TX power, and mode-aware filter width presets — unsupported controls auto-hide.
- Native **Icom CI-V serial** support (IC-7300/705/7610 and more) without Hamlib.
- **HF Nets & SWL Directory** ("Dir" tab, tap to tune) and Wake Lock on ECHOCAT (v1.0.16).
- ECHOCAT **Club Station Mode** beta (v1.0.8): callsign + password login with member badges.
- **MacLoggerDX** UDP forwarding on port `9090` (v1.0.7).

### v1.0 — March 9, 2026

- First stable release — "45 releases since launch."
- **Spacebar PTT** for ECHOCAT (iPad keyboards) and a cleaner Welcome screen.
- ECHOCAT audio settings in Quick Settings; new "Radio" filter for band/mode.

### ECHOCAT launch — March 4, 2026

- **ECHOCAT**: control the rig from a phone browser over a **Tailscale** VPN — 100% free.
- Requires Tailscale on the shack PC and phone; browse to `https://100.x.y.z:7300`.
- Per-rig RX/TX audio channels set in the Rig dropdown.
- Followed the same week by the **DX Terminal** cluster window with one-click QSY (v0.9.39) and **NG3K ADXO** DX-expedition spots (v0.9.40).

### v0.9.27 — March 2026

- **Activator Mode** (introduced in late-February rolling builds): activator log, RBN view of your own CQ pickups, and a sortable logbook with filtered ADIF export.
- Daily QSO **milestone celebrations** (10/25/50/100/150/200/250, with 500 as mega).
- WSJT-X auto-log now forwards to external logbooks; new Grid column; 2-fer double-logging fix.

### v0.9.22 — February 2026

- `F5` checks for a new version; **TCP rigctl** support.
- **DXCC tracker** by band and mode, built from your imported logbook.
- Event tracking: **WAS 250**, **CQ WW 160m**, and pre-loaded **13 Colonies**.
- POTA/DX pill column; QRZ request-flooding bugfix.

### v0.9.9 — February 2026

- **Auto-update** introduced — "the last version you have to download."
- Portable `.exe` still offered alongside the installer.

### v0.9.7 — February 2026

- **Serial CAT** using the Kenwood protocol, bypassing Hamlib (QRPLabs QMX/QDX and similar).
- **Worked Station Tracking**: green check, muted spots, auto-skip in scan, "Hide already-worked" — plus ADIF import (LoTW/QRZ) and POTA hunted-parks CSV import.
- **Light/dark theme** toggle and a continent filter (AF/AS/EU/NA/OC/SA).
- **Logbook forwarding** to N1MM+ (UDP `2333`), N3FJP (TCP `1100`), HRD (TCP `7826`), and Log4OM 2.
- **SmartSDR panadapter spots** (TCP `4992`); RBN watchlist spots in the main spot table.
- **POTA re-spot** feature included in the same build.

### v0.9.6 — February 2026

- **Ham Radio Deluxe** and **Log4OM 2** logging integrations go live.
- Pre-auto-update era: manual uninstall/reinstall required to upgrade.

---

For full release notes on every build, see the **#announcements** channel on the POTACAT Discord.
