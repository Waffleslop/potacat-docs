# WebSDR, KiwiSDR and RTL-SDR Receive

POTACAT can listen through a receiver other than your radio: a **KiwiSDR** or **WebSDR.org** station on the internet, or an **RTL-SDR** on your own network. It follows your radio's dial, so you can hear a signal from another location (handy when local noise covers it) while you transmit on your own rig. No radio license is needed just to listen.

## Add a receiver

Open **Settings > Station > WebSDR**. Each row has a **Label** (any short name) and a **Host** as `host:port`.

- Click **Browse…** to pick a station from POTACAT's built-in list (**Choose an SDR Station**), or type a host yourself. Port `8073` means a KiwiSDR; other ports are treated as WebSDR.org.
- **Add SDR** adds another row.
- The help text links to the live directories of [KiwiSDR](http://rx.linkfanel.net) and [WebSDR.org](http://websdr.org) receivers if you want one that isn't in the list.

## Listen through it

In the **VFO window**, open its ⚙ settings and, under **WebSDR**, turn on **Enable WebSDR receive** and choose the station. **Add or edit SDRs** takes you back to the list above. While you listen through an SDR, the VFO window shows an **SDR RX** badge.

## KiwiSDR notes

- From POTACAT 1.13.8, KiwiSDR receivers on firmware 1.902 work again. Earlier versions went silent on them.
- Some KiwiSDR owners allow listening only on the receiver's own web page. POTACAT says so when you connect to one, instead of going quiet.

## An RTL-SDR on your network (rtl_tcp)

From POTACAT 1.13.8, the same list takes an **rtl_tcp** server: an RTL-SDR running `rtl_tcp`, or an SDRplay running `rsp_tcp`, on this PC or on another computer such as a Raspberry Pi by your antenna. Type it as `host:port`, for example `192.168.1.50:1234`. POTACAT recognises it when it connects and demodulates the signal itself: USB, LSB, CW, AM and FM.

- It sends about 4 Mbit/s, so use it on your own network, not over the internet.
- If the same SDR is your band scope (**Settings > My Rigs** > edit the radio > **Band scope from an SDR**), listening uses that connection and its gain and direct sampling settings.
- Tune outside your radio's range (NOAA weather, a 2 m repeater on an HF rig) and POTACAT tunes only the SDR and won't transmit; tune back into range and the radio is back.
