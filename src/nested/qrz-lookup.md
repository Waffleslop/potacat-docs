# QRZ Lookup

If you enter your QRZ credentials in Settings → Station, POTACAT enriches spots with operator names, grid squares, state, county, and country from QRZ.

- **Hover tooltip** — hover over a callsign in the table to see the operator's name
- **Nickname preference** — POTACAT uses the QRZ nickname field when available (e.g. "Bob" instead of "Robert")
- **Log dialog** — the operator name is shown in a read-only field



## What QRZ Fills In

- **County** goes to the county field only for US stations (from 1.14.0). QRZ gives a county for everyone; for a KH8, for example, it is "American Samoa". A county you type yourself is always kept.
- **Portable calls resolve to where they operate:** W1AW/KL7 is Alaska, and KL7 and KH8 contacts take QRZ's DXCC entity instead of the mailing address.
- **A slow QRZ answer still fills the contact.** When QRZ answers after the contact is saved, its name, state and grid are added to the saved contact. Anything you typed is kept.
- **The QRZ status line says what's wrong:** signed in without an XML subscription, a wrong password, or no such account.
