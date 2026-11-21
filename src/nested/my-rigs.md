# My Rigs

POTACAT supports multiple saved rig profiles. Each profile stores a name and connection settings. Switch between rigs by clicking the CAT status pill in the status bar and selecting from the rig list.

## Your Radio's Bands

> **New in POTACAT 1.13.3.**

POTACAT offers only the bands the active radio can use: in spots, the band buttons, the VFO window, FT8, SSTV, JS8, Winlink's gateway list and ECHOCAT Web. A radio POTACAT knows uses its model's band list. An unknown model shows every band.

To change the list, open **Settings > My Rigs**, edit the radio, and use **Check all bands you can use with this radio**:

- **Tick a band** the model doesn't list, such as 4 m on a European IC-7300 or FT-710, or 2 m behind a transverter. It comes back everywhere.
- **Untick a band** you never use, to hide it.
- **Use this model's bands** puts the model's list back.

Once you have changed the ticks, your list wins over the model's.

> **Note:** After updating to 1.13.3, check this list if you use a band your radio's standard model doesn't cover. Your logbook and award views are never filtered.



## Full Power (W)

> **New in POTACAT 1.14.0.**

Some radios present themselves as a different, bigger radio. A 5 W Hermes Lite 2 run through deskHPSDR, piHPSDR or Thetis shows up as a 100 W TS-2000, so POTACAT's power slider, meter and log are wrong.

For such a radio, open **Settings > My Rigs**, edit it, and fill in **Full power (W)**, under **Radio Model**, with what the radio makes at full drive (for example `5`). The **TX Pwr** slider, the meter and the log then show real watts, through Hamlib too.

- **Leave it blank** where power already reads right. Blank keeps the model's own power.
- **With a Guest Pass**, a power cap above the radio's full power gives the radio's full power: a 5 W radio under a 25 W pass shows and logs 5 W.

## Amplifier Drive Limit

> **New in POTACAT 1.14.6.** Not yet tried on a radio.

For an amplifier that needs little drive, open **Settings > My Rigs**, edit the radio, tick **An amplifier is connected: limit the drive power** and fill in **Never drive above (W):**.

- POTACAT never sets this radio's power above that: not from a power slider, FT8, WSPR, Winlink, Tune, a guest or ECHOCAT. Every power slider stops there.
- If the radio reports more, from its own knob or another program, POTACAT turns it back down.
- Commands you type yourself in the rig panel's Commands tab are sent as written.
- It is off unless you set it.

## Power Off

This section describes POTACAT 1.14.7.

Whether **Power Off** is shown depends on how the radio is connected, unless you choose yourself:

- **Shown** for a radio on a direct serial port (Yaesu, Kenwood, Elecraft, Icom CI-V) and for a radio on a Yaesu SCU-LAN10.
- **Hidden** for a radio reached through Hamlib or rigctld, and for every other connection: TCP CAT, the Elecraft K4 over the network, Icom CI-V over TCP and Icom Network. It is also hidden for the Yaesu FTX-1, which cannot be switched on over CAT.

To choose yourself, open **Settings > Radio**, click **Edit** beside the rig, and tick or untick **Show Power Off for this radio**. Your choice wins either way and is kept. A line under the box says whether POTACAT can turn that radio back on, for example *POTACAT can turn this radio back on over its serial connection.* or *POTACAT cannot turn this radio back on through Hamlib. You will need the radio's own power button.*

**Power On** only works if the radio keeps its computer connection alive while it is off. If yours does not, untick the box or keep the radio's power button within reach.

In 1.14.6 the box was named **Allow Power Off for a radio POTACAT cannot turn back on**, and Power Off was hidden for most radios on a USB cable. A rig where that box was ticked keeps Power Off.

## Transmit Audio Input (Kenwood)

> **New in POTACAT 1.14.6.**

For the TS-480, TS-590S/SG, TS-890S and TS-990S, **Transmit audio input:** in **Settings > My Rigs** names the socket your sound card interface is plugged into:

- **Rear (data / ACC2 socket)**
- **Front (microphone jack)**
- **Ask on first transmit**

POTACAT tells the radio which one to send each time it transmits. The wrong one puts a carrier on the air with no audio. A TS-480 asks you on its first transmit.

## A Band-Scope SDR on the Radio's IF Output

From 1.14.6, under **Band scope from an SDR**, **The SDR is connected to:** has two choices:

- **An antenna, or the radio's RX OUT (moves with the dial)**
- **The radio's IF output (stays on one frequency)**, with **IF frequency (Hz):** from the radio's manual. The picture then holds still as you tune.
