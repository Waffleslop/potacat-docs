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
