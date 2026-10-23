# Q-Link for the Commodore 64 Ultimate

**Public Release Beta 1 (`v1.0.0-beta.1`, 2026-10-23).** One disk image with everything: the Q-Link client, the People
Connection games, RabbitJack's Casino, **Club Caribe** and **Super-Q**, for the Ultimate's built-in SwiftLink-type modem (a 6551
ACIA at `$DE00`). The client is **pre-configured**: it dials `qlink.kd4cbm.us` port `5190` by itself, so there is no modem
command, host name or phone number to type. Tested on a **Commodore 64 Ultimate**; the Ultimate 64 and Ultimate-II(+) emulate the
same modem and should work, but are untested. This is a beta: please report anything odd, and where it happened.

| Image | What it is |
|---|---|
| **`qlink-ultimate-swiftlink-de00.d81`** | **The Ultimate image.** Client, both game disks, the casino, Club Caribe (both sides) and Super-Q on one 1581 image: no disk swaps. Needs the Ultimate's **REU** (2 MB or more) |
| `qlink-ultimate-swiftlink-de00-16mb.reu` | Optional: Q-Link's REU store for that D81, already filled, for **REU Size 16 MB**: even the first session after power-on is fast |

## Set up the Ultimate
1. Ultimate menu, **C64 and Cartridge Settings**:
   * the modem interface (ACIA / SwiftLink emulation) at **`$DE00`**, interrupt **NMI**. Nothing else may use `$DE00` (for example
     a Retro Replay cartridge);
   * **RAM Expansion Unit = Enabled** (not "GeoRAM Mode": that switches the modem off), **REU Size 2 MB or more, 16 MB
     recommended**. **The REU is for Q-Link only**: Q-Link uses the whole REU, so do not use other REU programs or RAM disks
     with it.
2. Make your own **writable working copy** of the D81 (the client saves your account on it, and Club Caribe updates its pictures
   on it) and mount it in drive A. If the Ultimate does not switch drive A to 1581 by itself, set **Drive A Type = 1581**.
3. Start with `LOAD"QUANTUM",8,1` (`LOAD"*",8,1` only works on a freshly powered drive). Q-Link checks the REU first and shows
   "Q-Link uses the whole REU (16 MB)." (the first time also "New REU store set up"). Then it dials by itself.
4. **First visit:** choose a screen name and answer the four questions (name, city, state, country); the client saves your
   account to your working copy. **Later visits:** boot it and you are signed straight in. Keep that copy: your account lives on it.
5. **Optional, faster first session:** with REU Size 16 MB, select `qlink-ultimate-swiftlink-de00-16mb.reu` in the Ultimate's file
   browser and choose **Load into REU** (once), or **Preload into REU** with **REU Preload** on (at every power-on). Use it only
   with this D81 and REU Size 16 MB; with another size Q-Link simply sets up a new store and fills it as you go.

The connection is raw (the Ultimate's modem does no Telnet translation), so casino balances such as 255 are safe.

## Where things are
* **People Connection** (chat): F1 on People Connection at the main menu.
* **Super-Q**: hold **C=** and press **F1** on People Connection (the main menu says so: `C=+F1: Super-Q`); keep C= held until the
  screen changes. To leave: F7 > **Return to Q-Link**, then RETURN at "make sure your Q-Link disk is in the drive" (it is: the
  same D81). You are back at the main menu.
* **Games and RabbitJack's Casino**: People Connection > F7 > Play or observe an online game > Start a game. No disk prompts.
* **Club Caribe**: the same games list > Club Caribe. No disk to insert and no key to press: you appear in Populopolis. Joystick
  in **port 1**; fire + up / down / right / left = GO / DO / GET / PUT; F1 = ghost. **SHIFT + RUN/STOP** takes you back to People
  Connection. If the connection drops while you are there, leaving shows "Connection lost." after about 50 seconds; Q-Link then
  shows its own "connection broken" screen: press F5 and sign on again.

## Known issues (beta 1)
* After **Super-Q > Return to Q-Link**, the main menu does not show the `C=+F1: Super-Q` line (it does after sign-on). C= + F1
  works the same either way. Fixed in the next beta.

## What is different from the original disks
- A replacement RS-232 driver for the 6551 ACIA (our own code) in the client, the games, the casino, Club Caribe and Super-Q;
  when the line drops it stops sending, so **F5 after signing off returns to BASIC** instead of freezing.
- The client's dialer dials `host:port` from the disk (`qlink.kd4cbm.us:5190`); the image's user block holds only those dial
  settings, no account.
- One 1581 image instead of eight 1541 disks: the loader reads the 1581 directly and keeps what it loads in the REU.
  Club Caribe's own fast disk code was written for the 1541; the image carries a 1581 version of it, and Club Caribe's picture
  disk sits on the image's last tracks. Super-Q's People Connection files are on the image under their own name; holding C=
  picks them.
- The fixes of the user-port set (the random main-menu freeze, the casino's "go to another table" fix, Club Caribe's corrected
  side 1) plus two latent raster fixes, and two 1986 Club Caribe fixes (polled sending, packet numbering after a link reset).
- Built from the same archive disks as the user-port set; nothing else is changed.

## The earlier per-disk SwiftLink set (tester betas)
`qlink-client-v4-swiftlink-de00.d64`, `qlink-games-1-swiftlink.d64`, `qlink-games-2-swiftlink.d64`, `qlink-casino-swiftlink.d64`
and `club-caribe-side1-swiftlink-de00.d64` (with [`../club-caribe-side2.d64`](../club-caribe-side2.d64)) are the tester betas'
one-disk-per-side images for the same modem: no Super-Q, no REU store, disk swaps as on the original. They stay here for testers
who use them; new members should use the D81. Accounts do not move between the two: an account made on one is not on the other.

Changes: [`../CHANGELOG.md`](../CHANGELOG.md). Checksums: [`../SHA256SUMS`](../SHA256SUMS).
