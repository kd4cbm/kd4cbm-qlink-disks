# Q-Link disks for the Ultimate's SwiftLink (beta)

**Beta.** These images run Q-Link through a **SwiftLink-type ACIA** (a 6551 cartridge modem interface) instead of a user-port
modem. Tested on the **Commodore 64 Ultimate**; the Ultimate 64 and Ultimate-II(+) emulate the same ACIA but are untested. The client is **pre-configured**: it dials
`qlink.kd4cbm.us` port `5190` by itself, so there is no modem command, host name or phone number to type.

| Image | What it is |
|---|---|
| `qlink-client-v4-swiftlink-de00.d64` | Q-Link client V4 with the SwiftLink driver, ACIA at **`$DE00`**, pre-configured to dial `qlink.kd4cbm.us:5190` |
| `qlink-games-1-swiftlink.d64` | People Connection games, disk 1, with the SwiftLink driver |
| `qlink-games-2-swiftlink.d64` | People Connection games, disk 2 (Checkers, Reversi), with the SwiftLink driver |
| `qlink-casino-swiftlink.d64` | RabbitJack's Casino with the SwiftLink driver |

Use these four **together**: the user-port disks in the folder above and these do not mix in one session.
**Super-Q and Club Caribe are not available this way yet**: they still bring their own user-port drivers.

## Set up the Ultimate
1. Enable the modem interface (ACIA / SwiftLink emulation) at **`$DE00`**, interrupt **NMI**.
   Nothing else may use `$DE00` (for example a Retro Replay cartridge).
2. Make your own **writable working copy** of the client image and boot it: `LOAD"*",8,1`.
3. It connects on its own. **First visit:** choose a screen name and answer the four questions (name, city, state, country);
   the client saves your account to the disk. **Later visits:** boot and you are signed straight in.
4. When Q-Link asks for a game disk or the casino, mount the matching `-swiftlink` image and follow the prompt.
   In the casino menu pick **RabbitJack's Casino**.

The connection is raw (the Ultimate's modem does no Telnet translation), so casino balances such as 255 are safe.

## What is different from the user-port disks
- A replacement RS-232 driver for a 6551 ACIA (our own code) in the client, the games and the casino; the hang-up points and
  the disk loader call it. When the line drops (sign-off, or the server closes the connection), it stops sending, so
  **F5 after signing off returns to BASIC** instead of freezing.
- The client's dialer has a new type that dials `host:port` from the disk; this image has `qlink.kd4cbm.us:5190` stored
  in it (the user block holds only those dial settings, no account).
- Built from the same archive disks as the user-port set; nothing else on the disks is changed.

## Tested
In VICE (ACIA at `$DE00`): new member sign-up with no input, returning member sign-in, lobby and chat, a game
(Four in a Row), RabbitJack's Casino and its own sign-off, F5 to BASIC, also with the line drop simulated. On a
Commodore 64 Ultimate: sign-off and F5 to BASIC. Please report anything that freezes, and where.

Checksums are in `../SHA256SUMS`.
