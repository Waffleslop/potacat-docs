# Sharing Your Radio with Other Programs

POTACAT can run alongside a logger, a cluster program or a control program such as Win4Yaesu, all following the same radio. This page shows how.

## The one rule: one program per serial port

**Only one program can hold a serial (COM) port at a time.** If Win4Yaesu, a logger or WSJT-X already has the radio's port open, POTACAT can't open it too. Windows answers with **"Access denied"**, and Test Connection fails. POTACAT 1.13.10 and later say that another program holds the port.

"Access denied" doesn't mean a permissions problem or a broken driver. It means another program got to the port first.

There are four ways to share the radio. Pick one.

| Way | How it works | Use it when |
|---|---|---|
| **Virtual COM ports** | The program that holds the radio (Win4Yaesu, for example) gives each other program its own virtual port | You already run Win4Yaesu, or another program must own the radio |
| **A port splitter or virtual pair** | VSPE, com0com or similar make extra ports that all reach the radio | No program on your PC offers virtual ports |
| **flrig or rigctld** | flrig or rigctld holds the radio; POTACAT and the other programs connect to it over the network | You already use flrig or Hamlib |
| **POTACAT as the hub** | POTACAT holds the radio; loggers take POTACAT's QSOs and control the radio through it | POTACAT is your main program |

## Win4Yaesu: give POTACAT its own virtual port

Win4Yaesu holds the radio's real CAT port and can give each extra program its own virtual COM port. POTACAT, Log4OM, HolyCluster and other programs can then all stay open and follow the radio together.

**POTACAT doesn't use OmniRig, and doesn't need to.** If your other programs reach the radio through OmniRig, leave OmniRig set up exactly as it is. You don't need to change anything in OmniRig for POTACAT.

1. **In Win4Yaesu,** set up one more virtual COM port for a third-party program. Note the number of the end the other program opens, which is the one POTACAT will use. (Win4Yaesu's own help covers its third-party ports.)
2. **In POTACAT,** open **Settings > My Rigs**, edit the rig (or add one), and choose **Serial CAT (Kenwood / Yaesu)**.
3. Set **Radio Model** to your radio, for example **FTDX10**.
4. Under **Serial Port**, pick the virtual port. **Virtual ports often aren't in the list**, so type its name, such as `COM11`.
5. Set the **baud rate** to the one Win4Yaesu shows for that virtual port, then **Save**.
6. **Check it:** turn the radio's dial and POTACAT's frequency follows; click a spot and the radio tunes.

> **Note:** The two port numbers will look unrelated. Win4Yaesu holds the radio's own port (say `COM16`) and POTACAT uses the virtual one (say `COM11`). That is correct. **Don't point POTACAT at the radio's own port**: Win4Yaesu holds it, and you'll get "Access denied".

Once this works, [ECHOCAT](../echocat.md) on your phone drives the radio through POTACAT as usual, with nothing more to set up on the radio side.

If you'd rather build the virtual ports yourself with com0com, see [Win4Yaesu Setup](win4yaesu-setup.md).

## Port splitters and virtual port pairs

When no program on your PC hands out virtual ports, a splitter can:

- **VSPE** (Virtual Serial Ports Emulator) has a splitter that lets several programs open copies of one real port.
- **com0com** makes a pair of linked virtual ports: whatever one program writes to one end, the program on the other end reads. It needs a program in the middle that holds the real port.

Point POTACAT at its own port from the splitter, and type the port's name if it isn't in the list. com0com doesn't work inside a Windows virtual machine; VSP Manager is an alternative there.

## flrig or rigctld

Here flrig or rigctld holds the radio, and every program, POTACAT included, connects to it over the network on this PC:

- **flrig:** in POTACAT, choose **FLRig (a shared radio)** as the connection type, with host `127.0.0.1` and port `12345` (flrig's default). Your logger or fldigi connects to flrig the same way. Filter width, CW keying and the radio's menus stay in flrig.
- **rigctld:** run `rigctld` for your radio yourself, then choose **rigctld Network** in POTACAT with its host and port (`127.0.0.1:4532` by default). See [rigctld Network](rigctld-network.md).

> **Note:** On the **Other Rig (Hamlib)** connection, POTACAT starts its own rigctld on port 4532. If another program also runs a rigctld on 4532, change POTACAT's **rigctld Port** to an unused one, such as `4534`. See [rigctld port conflicts](cat-control-issues.md#rigctld-port-conflicts).

## POTACAT as the hub

If POTACAT owns the radio, other programs don't need the COM port at all:

- **Logging:** loggers take POTACAT's QSOs over UDP or as ADIF. Turn off rig control in the logger and see [Logbook Forwarding](logbook-forwarding.md).
- **WSJT-X:** set its radio to **Hamlib NET rigctl** at `127.0.0.1:4532`, and open POTACAT first. Or use POTACAT's built-in [JTCAT](jtcat.md) instead.
- **N1MM+ and other loggers that speak TS-2000:** POTACAT can act as a TS-2000 over TCP. See [Let N1MM+ control the radio](../radio-setup.md#let-n1mm-or-another-logger-control-the-radio).

## Still "Access denied"?

- Close every other program that might open the radio's port, then click **Test Connection** again. Common ones: loggers with rig control on (Log4OM, ACLog, N3FJP, HRD, World Radio League), WSJT-X, flrig, Win4Yaesu, the radio maker's own control program.
- Check you picked the **virtual** port, not the radio's own.
- More checks are in [CAT Control & Test Connection](cat-control-issues.md).
