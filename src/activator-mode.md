# Activator Mode

Switch to Activator mode from the Settings quick dropdown in the toolbar, or in Settings → App Mode.

Activator mode replaces the hunter table with a streamlined interface for running a POTA/SOTA/WWFF activation.

## Starting an activation

Enter your park reference(s) when you create the activation. For an n-fer (multiple overlapping parks), enter *every* reference up front — this matters for exporting later (see below). The multi-park dialog (**Ctrl+M**) keeps the park you've already typed, and comma-separated park lists auto-fill the country prefix (`US-`, `CA-`).

> **Tip:** Want to practice without confusing hunters? Activate the **K-TEST** test park reference, then QRT it on the POTA spot page when you're done.

### GPS park pick and offline maps (mobile app)

The mobile app's Activator Mode can pick nearby parks by GPS and stores offline POTA maps — downloading a park takes only seconds, so grab it before you drive out of coverage. The park list itself is downloaded and refreshed about monthly, so park-name lookup works offline too; offline callsign-to-name matching relies on the QRZ cache built during normal use. A **SPOTS** tab sits right next to the **ACT** tab so you can hunt park-to-park without leaving your activation.

### Self-spotting

You can self-spot straight from Activator mode — the equivalent of pota.app's **Add Spot** (a live spot). POTACAT does not declare your activation on the POTA website: announcing future plans (pota.app's **Add Activation**) and the final log upload are things you do on pota.app yourself.

## Logging during an activation

Any logging that occurs while an activation is open is added to the activation automatically. That includes QSOs you log from the spot table while hunting park-to-park — they count toward your activation's QSO total and keep the activation fields, so your `MY_SIG_INFO` stays intact when you flip between hunting and activating.

Clicking a spot while in Activator mode auto-fills the callsign and park reference in the logging form. The form also includes a hunter **State** field, pre-filled from the callsign lookup and editable before you save.

> **Note:** The auto-add only applies while the activation is open — there's no way to retroactively add previously logged QSOs to an activation.

## The QSO counter and UTC midnight

If your activation spans two UTC days, the QSO counter resets at `0000Z`. That's deliberate — POTA treats each UTC day separately, so the counter starts over for the new day.

## n-fers and multi-program activations

- **n-fer (multiple parks):** enter every park reference when you create the activation. POTACAT writes the correct per-park `MY_SIG_INFO` records.
- **Multi-program (same park in POTA + WWFF + LLOTA, etc.):** enter all the references; POTACAT generates one ADIF per program.
- **Park-to-park:** the P2P park field accepts comma-separated lists too.

> **Warning:** pota.app's uploader can't yet handle a single multi-park ADIF. For an n-fer, export **one log per park** (from **Past** activations) and upload each file to pota.app separately.

## After the activation

There is no POTA API for uploading logs, so POTACAT can't submit your activation for you — export the ADIF and upload it at pota.app. You can export a single activation's ADIF from the **Logbook**.

### Share Image

To show off a past activation, click **Past**, pick the activation from the dropdown, then click **Share Image** — POTACAT generates a shareable QSO-map image of that activation.


