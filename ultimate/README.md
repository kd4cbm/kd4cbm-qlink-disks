# Q-Link disks for the Ultimate's SwiftLink (beta)

**Beta 6** (2026-10-23): new **single-disk D81** with Club Caribe on it (see "The D81" below). These images run Q-Link through a **SwiftLink-type ACIA** (a 6551 cartridge modem interface) instead of a user-port
modem. Tested on the **Commodore 64 Ultimate**; the Ultimate 64 and Ultimate-II(+) emulate the same ACIA but are untested. The client is **pre-configured**: it dials
`qlink.kd4cbm.us` port `5190` by itself, so there is no modem command, host name or phone number to type.

| Image | What it is |
|---|---|
| `qlink-client-v4-swiftlink-de00.d64` | Q-Link client V4 with the SwiftLink driver, ACIA at **`$DE00`**, pre-configured to dial `qlink.kd4cbm.us:5190` |
| `qlink-games-1-swiftlink.d64` | People Connection games, disk 1, with the SwiftLink driver |
| `qlink-games-2-swiftlink.d64` | People Connection games, disk 2 (Checkers, Reversi), with the SwiftLink driver |
| `qlink-casino-swiftlink.d64` | RabbitJack's Casino with the SwiftLink driver |
| `club-caribe-side1-swiftlink-de00.d64` | Club Caribe program disk (side 1) with a SwiftLink driver, ACIA at **`$DE00`**. **Tested on a real C64 Ultimate** (beta 5). Use it with the unchanged image disk [`../club-caribe-side2.d64`](../club-caribe-side2.d64) |
| `qlink-ultimate-swiftlink-de00.d81` | **Beta 6, new:** everything above on **one 1581 image**: client (pre-configured, dials `qlink.kd4cbm.us:5190`), both game disks, RabbitJack's Casino and **Club Caribe, both sides**: no disk swaps. Needs the Ultimate's **REU** (2 MB or more) |
| `qlink-ultimate-swiftlink-de00-16mb.reu` | Optional: Q-Link's REU store for that D81, already filled, for **REU Size 16 MB**: loaded into the REU, even the first session after power-on is fast |

Use these **together**: the user-port disks in the folder above and these do not mix in one session (Club Caribe's image
disk, side 2, is the one exception: it has no modem code, so the same `../club-caribe-side2.d64` serves both).
**Super-Q is not available this way yet**: it still brings its own user-port driver.

## The D81: one image, no disk swaps (beta 6)
`qlink-ultimate-swiftlink-de00.d81` holds the client, both game disks, the casino and Club Caribe (program and image disk) on a
single 1581 image, and keeps a copy of what you load in the Ultimate's **RAM Expansion Unit (REU)**, so places you have visited
load again in seconds.
1. Ultimate menu, **C64 and Cartridge Settings**: the modem interface at **`$DE00`**, **NMI** (as below); **RAM Expansion Unit =
   Enabled** (not "GeoRAM Mode": that switches the modem off); **REU Size 2 MB or more, 16 MB recommended**.
   **The REU is for Q-Link only**: it uses the whole REU, so do not use other REU programs or RAM disks with it.
2. Make your own **writable working copy** of the D81 (the client saves your account on it, and Club Caribe updates its pictures
   on it) and mount it in drive A. If the Ultimate does not switch drive A to 1581 by itself, set **Drive A Type = 1581**.
3. Start with `LOAD"QUANTUM",8,1` (`LOAD"*",8,1` only works on a freshly powered drive). Q-Link checks the REU first: "Q-Link
   uses the whole REU (16 MB)." (the first time also "New REU store set up"). Then it dials by itself, as the D64 client does.
4. **Club Caribe:** People Connection > F7 > Play or observe an online game > Start a game > Club Caribe. No disk to insert and no
   key to press: you appear in Populopolis. **SHIFT + RUN/STOP** takes you back to People Connection, again without a prompt.
5. **Optional, faster first session:** with REU Size 16 MB, select `qlink-ultimate-swiftlink-de00-16mb.reu` in the Ultimate's file
   browser and choose **Load into REU** (once), or **Preload into REU** with **REU Preload** on (at every power-on). Use it only
   with this D81 and REU Size 16 MB; with another size Q-Link simply sets up a new store and fills it as you go.
6. **Super-Q is not on the D81 yet.** For Super-Q use the D64 set and a user-port modem, as before.
Your D64 working copies and this D81 are separate disks: an account made on one is not on the other (sign up again, or keep
using the D64 set).

## Set up the Ultimate
1. Enable the modem interface (ACIA / SwiftLink emulation) at **`$DE00`**, interrupt **NMI**.
   Nothing else may use `$DE00` (for example a Retro Replay cartridge).
2. Make your own **writable working copy** of the client image and boot it: `LOAD"*",8,1`.
3. It connects on its own. **First visit:** choose a screen name and answer the four questions (name, city, state, country);
   the client saves your account to the disk. **Later visits:** boot and you are signed straight in.
4. When Q-Link asks for a game disk or the casino, mount the matching `-swiftlink` image and follow the prompt.
   In the casino menu pick **RabbitJack's Casino**.

The connection is raw (the Ultimate's modem does no Telnet translation), so casino balances such as 255 are safe.

## Club Caribe (beta)
1. In Q-Link, go to Club Caribe. Mount `club-caribe-side1-swiftlink-de00.d64` when asked for side 1, then a **writable
   working copy** of `../club-caribe-side2.d64` (the image disk stays in the drive while you play; the server updates it).
2. Controls: joystick in **port 1**; fire + up / down / right / left = GO / DO / GET / PUT; F1 = ghost.
3. **To leave, press SHIFT + RUN/STOP** (not CTRL+Q, as earlier betas said). Club Caribe then asks for the Q-Link disk: mount your client working copy again and follow
   the prompt; you are back in People Connection.
4. **Swap back within 5 minutes.** While the disks are swapped (entering and leaving), the server holds your session for
   5 minutes; after that it drops the connection and you have to sign on again.
5. **If the connection drops while you are in Club Caribe** (beta 4): when you leave, Club Caribe waits about 50 seconds
   for the server, then shows **"Connection lost. Insert Q-Link disk, press any key."** Mount your client working copy and
   press a key; Q-Link then shows its own "connection broken" screen: press F5 and sign on again. (Before beta 4 it waited
   forever.)
Tested on a **real C64 Ultimate** against the live server (beta 5): Q-Link -> Club Caribe -> the world -> SHIFT + RUN/STOP ->
Q-Link, session held through the disk swap. Also tested in VICE, including the line cut while in Club Caribe (the
"Connection lost." exit above).

## What is different from the user-port disks
- A replacement RS-232 driver for a 6551 ACIA (our own code) in the client, the games and the casino; the hang-up points and
  the disk loader call it. When the line drops (sign-off, or the server closes the connection), it stops sending, so
  **F5 after signing off returns to BASIC** instead of freezing.
- The client's dialer has a new type that dials `host:port` from the disk; this image has `qlink.kd4cbm.us:5190` stored
  in it (the user block holds only those dial settings, no account).
- The client has the same fix for a random freeze at the main menu as the user-port client (modules `0006` and `9904`,
  see the main README).
- Two more spots that copy the same raster bit back (harmless in normal use, fixed to be safe): the client's raster set-up
  (module `0012`, waits for raster line 0 itself before it saves the screen setting) and the casino's bingo start-up
  (module `010`, masks the bit before it turns the screen on).
- Club Caribe side 1: only its RS-232 code (file `MCMG`, `$1331-$143C`) is replaced, plus a call on exit that switches the
  modem's receive interrupt off before Q-Link loads again, and (beta 4) a time-out on the exit's wait for the server's
  answer: after about 50 seconds without one, the disk prompt reads "Connection lost." first. Beta 5: the RS-232 code
  sends polled, like the client (sending from the modem's transmit interrupt garbled packets on the Ultimate), and a fix
  for a 1986 Club Caribe bug: after a link reset it numbered its next packet one past the highest sequence number, so
  the server refused it and the world never loaded. Everything else in Club Caribe is unchanged.
- Built from the same archive disks as the user-port set; nothing else on the disks is changed.

## Tested
In VICE (ACIA at `$DE00`): new member sign-up with no input, returning member sign-in, lobby and chat, a game
(Four in a Row), RabbitJack's Casino and its own sign-off, F5 to BASIC, also with the line drop simulated. On a
Commodore 64 Ultimate: sign-off and F5 to BASIC. Please report anything that freezes, and where.

## Changes
- **Beta 6 (2026-10-23):** new: the single-disk **D81** (`qlink-ultimate-swiftlink-de00.d81`) with the REU store and Club
  Caribe on it, plus its optional 16 MB REU image. Club Caribe's own fast disk code was written for the 1541; the D81 carries a
  1581 version of it, and the image disk sits on the D81's last tracks. Tested in VICE (1581 drive: sign-on, Club Caribe in and
  out twice); a first run on a real C64 Ultimate looked good, a fuller hardware test is under way. The D64 images above are
  unchanged from beta 5.
- **Beta 5 (2026-10-21):** Club Caribe side 1 only: it now works on the real C64 Ultimate (beta 4's side 1 stopped at entry
  there). The quit key is **SHIFT + RUN/STOP**; earlier betas wrongly said CTRL+Q. The client, games and casino are
  unchanged from beta 3, so keep using your working copies.
- **Beta 4 (2026-10-21):** Club Caribe side 1 only: a dropped connection no longer freezes Club Caribe when you leave (it
  shows "Connection lost." after about 50 seconds and returns you to the Q-Link disk prompt). The client, games and casino
  are unchanged from beta 3, so keep using your working copies. The server update of the same day also brings you back to
  People Connection cleanly if Club Caribe fails to start (for example a disk error on side 1).
- **Beta 3 (2026-10-20):** new: Club Caribe side 1 for the SwiftLink (VICE-tested, not yet on real hardware). Client and
  casino: two latent raster fixes (modules `0012` and `010`); nothing else changes, the games are as in beta 1. A beta 2
  working copy keeps working; to keep your account, keep using it (same advice as for beta 1 below).
- **Beta 2 (2026-10-20):** client only: fix for the random freeze at the main menu after sign-on (the raster interrupt
  stopped). The games and casino images are unchanged from beta 1. Already signed up with beta 1? Your account lives on
  your working copy (track 18, sector 15), so a fresh beta 2 copy would start a new sign-up; if you want to keep your
  account, keep using your beta 1 copy for now (it only has the occasional freeze), or ask us to help move it.
- **Beta 1 (2026-10-20):** first release.

Checksums are in `../SHA256SUMS`.
