# Docs → Website reply: LoTW and standalone ECHOCAT (2026-10-21)

**From:** desktop session (Alan), standing in for docs. Committed locally in potacat-docs; **not pushed yet**. The pages go live when Casey pushes master (the Pages workflow publishes docs.potacat.com).

## Pages changed

| Page | Change | URL once pushed |
|---|---|---|
| `src/nested/lotw-upload.md` (new, under QSO Logging) | Setup (TQSL, certificate, Station Location), Settings > Logging > Upload to LoTW, per-activation signing with the park's grid and state (and what is held back), Download confirmations | https://docs.potacat.com/nested/lotw-upload.html |
| `src/faq.md` "Does POTACAT upload to LoTW?" | Yes, through TQSL; links the new page | https://docs.potacat.com/faq.html |
| `src/faq.md` "Is there a phone app?" | Still mainly a remote; the ACT tab works alone; links below | https://docs.potacat.com/faq.html |
| `src/echocat.md` note at the top + new "Activating without a desktop" section | What works on the phone alone, and what needs Cloud or the desktop | https://docs.potacat.com/echocat.html#activating-without-a-desktop |

Checked against desktop `renderer/index.html` (LoTW block), `main.js` (upload is button-only, no auto upload), `lib/lotw-split.js`, `lib/lotw-report.js`, and the app's `AppShell.tsx` / `state/activation.ts`.

## Left out

- **Local Rig** (on-device FT8/FT4 via a Digirig). The app offers it from the FT8 tab, but I didn't confirm it's ready to document for users. Casey's call; it's one bullet to add to the new echocat.md section.

## Desktop note from the app handoff

Done in potacat-dev f61de18a (not pushed, ships in the next desktop release): every activation export (single, per-park, Upload to POTA) names the file with the UTC date of the first QSO instead of the export time. An activation that crosses 0000Z takes the first QSO's date.
