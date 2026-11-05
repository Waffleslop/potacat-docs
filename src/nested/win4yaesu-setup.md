# Win4Yaesu Setup

If you use Win4Yaesu Suite, both programs need access to the radio's serial port, and only one program can hold it.

The simplest way is to let Win4Yaesu give POTACAT its own virtual COM port, as described in [Sharing Your Radio with Other Programs](sharing-your-radio.md#win4yaesu-give-potacat-its-own-virtual-port). POTACAT doesn't need OmniRig, so leave any OmniRig setup as it is.

To build the virtual ports yourself, use **COM0COM** (free virtual COM port driver):

1. Install COM0COM (signed 64-bit version)
2. Create a virtual port pair (e.g. COM18 ↔ COM19)
3. In Win4Yaesu: assign COM18 to an AUX/CAT port
4. In POTACAT: set up **Serial CAT (Kenwood / Yaesu)** on COM19, with the baud rate Win4Yaesu uses for COM18. COM19 may not be in the port list; type its name.

```
POTACAT ←→ COM19 ──(COM0COM)── COM18 ←→ Win4Yaesu ←→ Radio
```

Win4Yaesu caches radio state, so POTACAT's polling doesn't add load on the radio. Multiple programs can run simultaneously on separate AUX/CAT ports.

> **Warning:** Don't point POTACAT at the radio's own COM port while Win4Yaesu is running. Win4Yaesu holds it, and POTACAT gets "Access denied".


