# Other Rig (Hamlib)

**Best for:** Icom, Yaesu, and radios that don't speak Kenwood protocol.

POTACAT bundles **Hamlib 4.6.5** (rigctld) — no separate installation needed. Supports 200+ radio models.

1. Add a new rig → select **Other Rig (Hamlib)**
2. Search for your radio model
3. Choose your COM port and baud rate
4. Click **Test Connection**
5. Save

POTACAT spawns a `rigctld` process, connects via TCP, and translates commands to your radio's native protocol.

## Radio Unplugged or Switched Off

From 1.13.2, if the radio's COM port disappears, POTACAT says the port is not there and waits for it, then connects by itself when it comes back. Older versions repeated "link restored, link lost".

POTACAT also no longer offers a Hamlib model that is a bridge to another program (FLRig, TCI, NET rigctl) for a radio on a COM port, and corrects one already set to your radio's own model.

## Ten-Tec Jupiter and Argonaut V

These radios power their serial interface from the DTR and RTS lines. From 1.13.2, POTACAT raises both, the way ACLog's "Power Option = Both" does.

- **Model:** Ten-Tec TT-538 Jupiter (Hamlib 16002), at 57600 baud for the Jupiter.
- Leave **Disable DTR/RTS on connect** off.
