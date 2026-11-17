# Zeus and Thetis (TCI)

> **New in POTACAT 1.14.6.** Not yet tried on a radio. If you run it, please send a report from [Report a Bug](../community--support.md#report-a-bug).

POTACAT can run a radio through **Zeus** or **Thetis** over TCI, with no sound card and no audio cable. This is a rig type of its own. It is separate from [TCI Panadapter Spots](tci-panadapter-spots.md), which only puts spot markers on the panadapter.

## Set it up

1. Start Zeus or Thetis and connect it to your radio.
2. Enable TCI in that program. Use host `127.0.0.1` when it runs on this computer.
3. In POTACAT, open **Settings > My Rigs**, add a rig and choose **Zeus or Thetis (TCI server)**.
4. Fill in **Program:**, **Host:** and **TCI port:**. The port is `40001` for Zeus and `50001` for Thetis.
5. Leave **Start the receiver when POTACAT connects** ticked if POTACAT should start the receiver.
6. Press **Test connection**.

If the program is not running yet, POTACAT keeps trying every 5 seconds. With TCI off, or a different port, the test fails and nothing tunes.

## What works

- **Tuning and controls.** POTACAT tunes the radio, follows its dial and mode, reads the S-meter, and sets the filter, squelch, AGC, noise blanker, noise reduction and attenuator through the TCI server.
- **Receive audio.** The audio source is **TCI audio from Zeus or Thetis**. JTCAT decodes and draws its waterfall, the VFO window's monitor plays, and ECHOCAT hears the radio.
- **Band scope.** The band scope comes from the server's IQ stream, in the **More** menu, ECHOCAT Web and the app. If no IQ arrives within 3 seconds, it says so.

## Transmit

- **Zeus** transmits from JTCAT (FT8 and the other digital modes) and from ECHOCAT voice, using your phone's microphone.
- The **PTT** button, voice macros, CW, **Tune**, SSTV and the ATU do not key a TCI rig yet.
- Power on a TCI rig is a percentage of drive.
- **Thetis** is receive only for now, until a Thetis owner has confirmed transmit.
