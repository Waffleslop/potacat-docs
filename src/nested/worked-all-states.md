# Worked All States

> **New in POTACAT 1.13.2.**

POTACAT keeps track of the US states and Canadian provinces you have worked and confirmed, by band and mode, and tints them on every map. It does the same for countries.

## The Worked All States View

Open **More ▾ > Worked All States**. It lists every US state and Canadian province by band and mode: **blue** means worked, **green** means confirmed.

A state counts only when the QSO has its **STATE** field filled in. To fill it on contacts that don't have it, use **Update from LoTW** and **QRZ** (see [Filling in states](#filling-in-states) below). Australian states aren't tracked, because their codes collide with US ones.

## Tints on Every Map

On any map, these keys switch the tints:

| Key | Action |
|-----|--------|
| **F6** | Tint worked and confirmed states |
| **F7** | Tint worked and confirmed countries |
| **F8** | Change the band and mode the tints are about. By default they follow your radio. |

The box on the map holds the same switches and the counts. To hide the box, click **Worked** beside **Map** in the FT8 window, or in the title bar of the FT8 map pop-out. The tints and F6 / F7 / F8 keep working with the box hidden.

ECHOCAT Web shows the same tints on its maps.

## Filling in States

The map box has two buttons:

- **Update from LoTW** downloads your LoTW confirmations. Each one fills in the state and grid that the other station certified with LoTW. See [LoTW Upload](lotw-upload.md).
- **QRZ** fills in the state on older contacts, from the park or from a QRZ lookup. Each press makes up to 150 lookups, so a large log may need a few presses.

## Hunting Wanted States in FT8

FT8 decodes show a state badge on a station in a state you still need on that band and mode. In the JTCAT window's **AUTO** menu, pick **Hunt: Wanted states** and POTACAT answers only those stations. See [JTCAT](jtcat.md).
