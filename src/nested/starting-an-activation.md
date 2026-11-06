# Starting an Activation

1. **Enter your park reference** (e.g. `K-1234`) in the park input field — autocomplete helps you find parks
2. **Set your frequency** — type it or let POTACAT read it from your radio via CAT
3. **Select your mode** (CW, SSB, FT8, etc.)
4. Click **Start Activation**

A timer starts counting your activation time. Your contact count is displayed prominently.



## Logging Reliability

From 1.14.0, the Activator log never loses or doubles a contact. POTACAT waits at most about two seconds for QRZ, a contact you log while the previous one is still saving is saved right after it, in order, and the entry row is cleared only for the contact that was saved.

A contact switched to **General** never picks up the last park, here, in the Bottom Banner Logger or in ECHOCAT Web's Log sheet. Before, it could count as a false park-to-park. Contacts already logged that way need the park removed by hand, and re-uploading if they were sent to POTA.

WWFF and SOTA references are no longer flagged **Not in parks DB**: POTACAT has only POTA's park lists, so it checks POTA references only.
