# KD4CBM Q-Link disk images

Everything you need to sign on to **qlink.kd4cbm.us** (port **5190**) and use the games, the casino, Super-Q and
Club Caribe (Habitat). **Current release: Public Release Beta 1 (`v1.0.0-beta.1`)**; see [CHANGELOG.md](CHANGELOG.md) and the
[releases page](https://github.com/kd4cbm/kd4cbm-qlink-disks/releases).

**Which disks do I need?**
* **Commodore 64 Ultimate** (its built-in modem): the single D81 image in **[`ultimate/`](ultimate/)**. Start there.
* **Any other C64 with a user-port modem** (or VICE with a user-port modem): the standard 1541 `.d64` files below (via an SD2IEC,
  Ultimate, Pi1541 or a transfer cable).

## The user-port disk set

| Image | What it is | Needed for |
|---|---|---|
| `qlink-client-v4.d64` | Q-Link client, version 4 (disk name `Q-LINK VERSION4`) | everything: boot this first |
| `qlink-games-1.d64` | People Connection games, disk 1 (`QGAMES`) | the online board and card games on this disk |
| `qlink-games-2.d64` | People Connection games, disk 2 (`QGAMES2`) | Checkers and Reversi |
| `qlink-casino.d64` | RabbitJack's Casino (`DATA`) | the casino lounge and its games |
| `qlink-superq.d64` | Super-Q (`WIMEDATA`) | Super-Q rooms |
| `club-caribe-side1.d64` | Club Caribe program disk (`CLUB CARIBE`) | Club Caribe / Habitat |
| `club-caribe-side2.d64` | Club Caribe image disk (`HABITAT DATA`) | Club Caribe / Habitat (stays in the drive) |

## Commodore 64 Ultimate
The **[`ultimate/`](ultimate/)** folder has **one D81 image** for the Ultimate's built-in SwiftLink-type modem (ACIA at `$DE00`):
the client (it dials `qlink.kd4cbm.us:5190` by itself), the games, the casino, Club Caribe and Super-Q, no disk swaps; it needs
the Ultimate's REU. See [ultimate/README.md](ultimate/README.md). (The tester betas' per-disk SwiftLink images are there too.)

## Documentation
- **[CONNECTING.md](CONNECTING.md)**: modems (Zimodem and other Wi-Fi modems, tcpser, VICE), why you dial raw `ATD` and not
  `ATDT`, manual dial versus the Hayes-compatible auto-dial with a phone-book number, and your first sign-on.
- **[Member's Guide](docs/Q-Link-Reloaded-Members-Guide-Edition-1.pdf)** (PDF, Edition 1): the full guide to People Connection,
  the games, RabbitJack's Casino, Super-Q and the Music Connection, Club Caribe, mail and news, with a quick-reference card.
  Written for this server; where it says "ask the system operator for the corrected disk", the disks here are the corrected ones.

## Getting started (user-port set)
1. Make **your own working copies** of the images and keep these downloads untouched as a backup. The client writes
   your registration to its disk, and the Club Caribe image disk is updated by the server when you enter, so the
   working copies must be **writable**. Never share your working client disk: it holds your account details.
2. Point your modem (or modem emulator) at `qlink.kd4cbm.us`, port `5190`, and **dial raw** (`ATD`, not `ATDT`): see
   [CONNECTING.md](CONNECTING.md).
3. Boot the client: `LOAD"*",8,1`. New members register from the client; it saves your account to the disk.
4. When Q-Link asks for another disk (games, casino, Super-Q, Club Caribe), insert the matching image and follow the prompt.
   Club Caribe asks for side 1 first, then the image disk (side 2), which stays in the drive while you play.
5. Club Caribe controls: joystick in **port 1**; fire + up / down / right / left = GO / DO / GET / PUT; F1 = ghost.
   To leave Club Caribe press **SHIFT + RUN/STOP**, then put your Q-Link disk back in within 5 minutes.

## What is different from other copies
- **`qlink-client-v4.d64`**: the 2005 archive copy with its user block (track 18, sector 15) reset to the factory-blank
  state (the archive copy still held an old registration), and **a fix for a random freeze at the main menu** (2026-10-20):
  four BASIC lines in modules `0006` and `9904` turned the screen on and off with `POKE53265,PEEK(53265)...`, which can copy
  the current raster line into the raster-interrupt compare and stop the client's raster interrupt (no keyboard, the client
  waits forever, typically right after sign-on). Those lines now mask that bit; nothing else on the disk is changed.
- **`qlink-casino.d64`**: carries our change-table fix (index files `005` and `006`); without it, changing tables fails.
- **`club-caribe-side1.d64` / `side2.d64`**: built with the original Club Caribe kit. The kit writes the pointer to the
  `MCM` index byte-swapped, so a freshly built program disk recognises the image disk and then hangs; side 1 here has
  that pointer corrected (file `MCM` only).
- The other images are unchanged archive copies.

Checksums are in `SHA256SUMS` (`sha256sum -c SHA256SUMS`).

## Credits and rights
Q-Link, the Q-Link client, its games, the casino and Super-Q were created by Quantum Computer Services (later America
Online) and the game authors; these copies are provided for preservation and for testing this non-commercial revival.
Habitat / Club Caribe was created by Lucasfilm Games (Chip Morningstar, Randy Farmer, Aric Wilmunder, Gary Winnick and
others); its source and assets were released under the MIT licence by the Museum of Art and Digital Entertainment
(<https://github.com/Museum-of-Art-and-Digital-Entertainment/habitat>), and the live world is run with the NeoHabitat
project. If you hold rights to any of this material and want it removed, please open an issue.
