# Community & Support

**Website:** [potacat.com](https://potacat.com)

**Discord:** Join the community at [potacat.com/discord](https://potacat.com/discord) — get help, share your setup, request features, and chat with other POTACAT users.

**Support development:** If POTACAT helps you chase parks, consider supporting the project at [buymeacoffee.com/potacat](https://buymeacoffee.com/potacat).

**Author:** Casey Stanton, K3SBP

**License:** MIT. Bundles [Hamlib](https://hamlib.github.io/) (GPL v2).

## Report a Bug

This is the one place the docs describe how to report a problem. Other pages link here.

### From POTACAT (the best way)

1. Open **Settings** and click **🐞 Report a Bug** at the bottom of the tab list on the left.
2. A red banner says POTACAT is recording. **Reproduce the problem now**: key up, click the spot, do whatever goes wrong. POTACAT records a detailed log while you do.
3. Click **Copy Report** in the banner. The report goes to your clipboard; nothing is sent by itself.
4. Paste it into the **#bug-report** channel on [Discord](https://potacat.com/discord), with a sentence on what you expected and what happened.

The report includes your radio, how it is connected and the recent log, with your passwords left out, so we don't have to ask. **Never paste your `settings.json`** into Discord or anywhere public: it holds your passwords.

### If you'd rather use GitHub

Open an issue at [github.com/Waffleslop/POTACAT/issues](https://github.com/Waffleslop/POTACAT/issues) (the **Report Bug** link at the bottom of the POTACAT window goes there) and paste the report from step 3 into it.

### If POTACAT won't start, or runs with no window

- **Running headless (no window), for example on a Raspberry Pi:** there's no Report a Bug button. Copy the log file off the computer as described in [Getting a log without the window](nested/installation-issues.md#getting-a-log-without-the-window-headless--raspberry-pi), and attach it on Discord or GitHub.
- **On a Mac, it opens and quits at once:** run it from Terminal to see the error, as in [Installation Issues: The app opens and immediately quits](nested/installation-issues.md#the-app-opens-and-immediately-quits), and paste what it prints.
- **Otherwise:** the log is `session.log` in the [settings folder](nested/installation-issues.md#where-settings-live-and-factory-reset); attach that.

### Problems with the ECHOCAT app

The ECHOCAT phone app is a remote for POTACAT on your computer, so most problems are fixed there. Update POTACAT first, then report from POTACAT as above.
