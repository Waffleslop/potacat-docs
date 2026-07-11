# ADIF File

QSOs are saved to a local ADIF file. Set the file path in Settings → Logging. Each QSO is appended as a standard ADIF record with fields including CALL, FREQ, MODE, BAND, RST_SENT, RST_RCVD, QSO_DATE, TIME_ON, OPERATOR, TX_PWR, SIG_INFO (park ref), and QRZ-derived fields (NAME, STATE, CNTY, GRIDSQUARE, COUNTRY).

> **Warning:** Changing the ADIF file path starts a new, empty log at the new location. Your old file is not deleted — it just stops being written to — so any QSOs you log afterward land only in the new file. Move or back up the old file deliberately if you want your history in one place.

## Field Notes

- For POTA contacts, `STATE` records the **park's** state (not the activator's home state from QRZ), and the county (`CNTY`) is intentionally left blank — county data isn't queryable for parks. County hunters shouldn't expect a county on POTA hunts.
- FT4 and FT2 QSOs are exported the ADIF-correct way, as `MODE=MFSK` with `SUBMODE=FT4` (or `FT2`). POTA's uploader rejects files that use a plain `MODE=FT4`, so keep this form if you ever hand-edit an export.

## Activation Exports

You can export an ADIF for an individual activation from your past activations.

> **Note:** For a multi-park (n-fer) activation, the POTA uploader can't yet process a single multi-park ADIF file. Enter all the park references when you create the activation — POTACAT writes correct per-park `MY_SIG_INFO` records — then export a separate log for each park and upload each file on its own.


