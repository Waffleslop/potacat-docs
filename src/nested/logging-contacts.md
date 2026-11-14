# Logging Contacts

The quick-log form at the top has:
- **Callsign** — type the hunter's callsign
- **RST Sent / Received** — split-digit input boxes with auto-advance (or single-field N1MM-style if enabled in Settings)
- **Hunter Park** — if the hunter is also at a park (park-to-park QSO), enter their reference. From 1.14.5 the field takes up to six parks, separated by commas, and typing a different callsign clears it, so an abandoned QSO's park is not carried into the next contact. A park typed over another one replaces it
- **Operator name** — auto-filled from QRZ lookup

Press **Enter** or click **Log** to save. The contact appears in the activation log table below.

Use **Alt+R** to reload the last contact into the form (handy for correcting mistakes).

## Contacts Logged Outside the Activation Screen

From 1.14.5, a contact logged during an activation from the log window (**Ctrl+L**, **Cmd+L** on a Mac) or from ECHOCAT appears in the activation list and its **Export ADIF**. Before, it was saved with your park but left out of both.

**A contact made before Start Activation can join it.** In the Logbook, turn on the **My Park** column (right-click the column header) and set the contact's park. It is then filed under that park's program, so **Stop Activation**, then **Past**, then **Resume** picks it up for the same UTC day. My Park takes one park per contact.

**A corrected park reaches POTA.app.** Since 12 November 2026, POTA.app reads the `POTA_REF` field ahead of `SIG_INFO`. From 1.14.5, editing the other station's park in the Logbook updates both. Before, only `SIG_INFO` changed, so the old park was still uploaded and credited.
