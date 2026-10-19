# Connecting to Q-Link Reloaded (qlink.kd4cbm.us, port 5190)

Q-Link expects a **Hayes-compatible modem at 1200 baud** on the user port. Today that "modem" is a Wi-Fi modem (Zimodem and
similar), the Ultimate's modem, **tcpser** on a PC, or VICE's emulated RS-232. They all end in the same place: a TCP connection
to `qlink.kd4cbm.us` port `5190`.

## The one rule: dial raw (`ATD`, not `ATDT`)

Q-Link's data contains the byte `$FF` (for example any casino balance of 255, 511, 767 ...). A modem in **Telnet mode** treats
`$FF` as a Telnet command and quietly removes it; Q-Link then rejects the damaged block and asks for it again, forever: the screen
freezes. So the connection must be **raw**:

| Modem | Raw | Telnet (avoid) |
|---|---|---|
| Zimodem | `ATD"qlink.kd4cbm.us:5190"` | `ATDT"..."` (the `T` switches on Telnet translation) |
| Zimodem | | `ATDP"..."` is worse: `P` translates the data to PETSCII |
| tcpser | `ATDT` or `ATD` both raw (tcpser only speaks Telnet if the far end asks, and Q-Link never does) | |
| VICE, direct | IP232 **off** | IP232 on, pointed straight at the server |

## How the Q-Link disk dials

When you start a **new** client disk, Q-Link asks how you connect and saves your answers (with your account) on the disk:

* **Manual dial**: Q-Link shows *"TYPE COMMANDS TO THE MODEM, THEN PRESS F1 WHEN CONNECTION IS MADE."* You type the dial
  command yourself, wait for `CONNECT`, press **F1**. **Recommended for Wi-Fi modems**: you control exactly what is sent.
* **A Hayes-compatible modem** (the "other Hayes" choice): Q-Link dials for you with `ATD` + `T` (tone) or `P` (pulse) +
  the phone number you gave it, for example `ATDT 5551212`. A modem that understands that number (tcpser's or Zimodem's
  phone book, below) connects you with no typing.

Q-Link cannot type a host name in auto-dial: it sends **digits only**. That is what a modem **phone book** is for: it maps a
made-up number such as `5551212` to `qlink.kd4cbm.us:5190`.

## Zimodem (and other Wi-Fi modems)

One-time setup, typed in a terminal program (for example CCGMS) before you start Q-Link:

```
ATB1200
ATS62=0
AT&W
```

`ATB1200` sets 1200 baud, `ATS62=0` keeps Telnet handling off, `AT&W` saves both.

**Manual dial (recommended):** choose manual dialing in Q-Link, then at its prompt type

```
ATD"qlink.kd4cbm.us:5190"
```

and press **F1** when the modem says `CONNECT`.

**Auto-dial (optional):** add a phone-book entry once, without the `T` modifier, then give Q-Link the number `5551212`:

```
ATP"5551212=qlink.kd4cbm.us:5190"
AT&W
```

Q-Link will send `ATDT 5551212` (or `ATDP` for pulse). Because Q-Link adds that `T`/`P` itself, whether your firmware then turns
on Telnet or PETSCII translation depends on the firmware. **If the casino freezes on a balance such as 255, switch to manual dial.**
Never choose pulse (`P`) with Zimodem.

Other Wi-Fi modem firmwares: use their raw/"no Telnet" dial form; check the manual for how they take `host:port`.

## tcpser (a PC acting as the modem)

Map a number to the server and let Q-Link auto-dial it:

```
tcpser -d /dev/ttyUSB0 -s 1200 -n 5551212=qlink.kd4cbm.us:5190
```

(`-d` is the serial port your C64 cable is on; on Windows a `COM` port.) Choose the Hayes-compatible modem in Q-Link with the
number `5551212`. Manual dial also works: `ATDTqlink.kd4cbm.us:5190`.

**tcpser with VICE:** start tcpser with an IP232 port instead of a serial port,

```
tcpser -v 25232 -s 1200 -n 5551212=qlink.kd4cbm.us:5190
```

and in VICE set RS-232 device 1 to `127.0.0.1:25232` with **IP232 on** (VICE and tcpser both speak IP232, which carries `$FF`
correctly). Keep tcpser's port on `127.0.0.1` or behind your firewall: a modem emulator dials whatever it is told to.

## VICE without tcpser

| VICE setting | Value |
|---|---|
| User port device | RS-232 (user port), device 1, **1200 baud** |
| RS-232 device 1 | `qlink.kd4cbm.us:5190` |
| IP232 | **off** |
| Drive 8 | your **working copy** of the client disk, on your own computer (not a network drive) |

VICE connects as soon as Q-Link opens the port, so choose **manual dial** and just press **F1**.

## Getting in

1. Boot your working copy of the client: `LOAD"*",8,1`.
2. A new disk asks for your modem setup and dial method (above), then connects.
3. **First visit:** choose a screen name (up to 10 letters and digits) and give your name, city, state and country. Q-Link writes your
   account number and access code to the disk, so the disk must be writable, and it is now **your key**: keep it, back it up, don't
   share it.
4. **Later visits:** boot, connect, and you are signed straight in.
5. Trouble: "Already logged in" after a dropped line: wait a minute and try again. Access code refused, or a lost disk: ask the system
   operator for a new access code and enter it with the `CHANGE ACCESS` program on the client disk.

More in the **Member's Guide** (`docs/`), chapters 1, 2 and 10.
