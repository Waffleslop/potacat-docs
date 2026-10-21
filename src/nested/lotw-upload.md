# LoTW Upload

POTACAT signs and uploads your log to ARRL's Logbook of the World (LoTW) with your own TrustedQSL (TQSL) install, and can download your LoTW confirmations back into the log.

## Before you start

1. Install [TrustedQSL](https://www.arrl.org/tqsl-download).
2. In TQSL, load your callsign certificate.
3. In TQSL, create a Station Location for your home station (**Station > Add/Edit Station Locations**).

POTACAT finds TQSL on its own. If it can't, Settings says "TQSL was not found"; install TQSL, then reopen Settings.

## Uploading

1. Open **Settings > Logging** and tick **Upload to ARRL Logbook of the World (via TQSL)**.
2. Pick your home **Station Location** from the list (it comes from TQSL).
3. Enter your **certificate password** only if your certificate has one.
4. Press **Upload to LoTW**.

The upload sends your whole POTACAT log, and TQSL's duplicate detection sends only what LoTW hasn't seen. You can press it as often as you like. QSOs LoTW already has are marked sent and counted as "LoTW already had".

### Activations are signed with the park's grid and state

Home QSOs are signed with the Station Location you picked. Each activation is signed separately, with its own park, grid and state, so a contact made in a park in another state never carries your home location.

The grid and state come from the QSO records, or from the parks database when the record has none. A US park batch with no single state, or any batch with no grid, is held back and listed in the result rather than guessed: an incomplete station record at LoTW can't be fixed later, while a held-back batch is one edit away. Add the missing grid or state in the Logbook and upload again.

## Downloading confirmations

1. In the same section, enter your **LoTW username** and **LoTW password**. This is your lotw.arrl.org website login, not the certificate password.
2. Press **Download confirmations**.

Confirmed QSOs get the L✓ mark in the QSO log window and count as confirmed in the [DXCC Tracker](dxcc-tracker.md). The first download pulls your full history; later ones fetch only new confirmations.
