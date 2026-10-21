# Website → Docs handoff: two out-of-date answers (2026-10-21)

**From:** POTACAT website session (Alan), 2026-10-21
**Repo:** `D:\Projects\potacat-docs`
**Casey approved this handoff on 2026-10-21.**

potacat.com is getting a POTA logging page (`/pota-logging-app/`) that links to these docs. Two answers in the docs contradict what the apps actually do. A code check of desktop 1.12.0 and ECHOCAT 1.5.3 found both.

## 1. LoTW upload has shipped

`src/faq.md:139–141` asks "Does POTACAT upload to LoTW?" and answers "Not yet — LoTW integration is in progress but hasn't shipped."

That is no longer true:
- **v1.10.5** added "Upload to LoTW" through the user's own TrustedQSL install (`potacat-dev/release-notes/v1.10.5.md:5`).
- **v1.11.7** signs each activation with its own grid and state (`release-notes/v1.11.7.md:20–23`; code in `lib/lotw-split.js`, `main.js` ~31821).
- LoTW confirmation download is in `lib/lotw-report.js`.

**Ask:**
- Rewrite the answer: yes, POTACAT uploads to LoTW through TrustedQSL (TQSL), which must be installed and set up with your certificate. Say where the button is, and that activations are signed with the grid and state of the park.
- Mention that confirmations download back.
- Add or link a setup page if none exists.

Check every detail against the desktop code; don't copy this note.

## 2. ECHOCAT logs activations on its own

**Where the docs are wrong:**
- `src/faq.md:20` says "the app is a remote control: you still run POTACAT on a Windows, Mac, or Linux computer connected to the radio".
- `src/echocat.md:12` says "The app is a remote control for POTACAT Desktop".

**What the code does:** since app 1.5.0 (2026-07-30), ECHOCAT logs an activation with no desktop running.
- `potacat-app/src/components/AppShell.tsx:265–270`, `src/state/activation.ts:17–21` (the 'local' backend).
- `src/components/QsoLogForm.tsx:263–268`.
- The app itself tells the user: "Local session — QSOs save on this phone and sync to the cloud" (`ActScreen.tsx:893–895`).

Casey confirmed on 2026-10-21 that the store builds include it.

**Ask:**
- Keep the remote-control explanation; it's still the main use. Add that the ACT tab works standalone in the field.
- **Works without a desktop:**
    - starting an activation and logging QSOs on the phone;
    - finding parks near you offline, using GPS;
    - POTA self-spotting over mobile data;
    - viewing and exporting the logbook.
- **Needs something else:**
    - QSOs reach the desktop and other devices through POTACAT Cloud sync, which is the paid plan;
    - the automatic re-spot when you log a QSO needs the desktop;
    - logging for another operator needs the desktop.
- **Local Rig:** FT8/FT4 on the phone through a Digirig, with no desktop and no network (`AppShell.tsx:297`, `SettingsRadioInUseScreen.tsx:469`). Mention it if it's ready for users; check with Casey if unsure.
- Update the FAQ answer and the echocat.md note together so they agree, and reword the "update POTACAT Desktop first" advice so it fits standalone users.

## Reply

Write `DOCS_TO_WEBSITE_HANDOFF_2026-10-21_LOTW_AND_STANDALONE_REPLY.md` here, listing the pages changed and their live URLs on docs.potacat.com. The website will link to them.
