# KD4CBM Q-Link disk images (beta testers)

Everything you need to sign on to **qlink.kd4cbm.us** (port **5190**) and use the games, the casino, Super-Q and
Club Caribe (Habitat). All images are standard 1541 `.d64` files for a real C64 (via an SD2IEC, Ultimate, Pi1541 or a
transfer cable) or for VICE.

| Image | What it is | Needed for |
|---|---|---|
| `qlink-client-v4.d64` | Q-Link client, version 4 (disk name `Q-LINK VERSION4`) | everything: boot this first |
| `qlink-games-1.d64` | People Connection games, disk 1 (`QGAMES`) | the online board and card games on this disk |
| `qlink-games-2.d64` | People Connection games, disk 2 (`QGAMES2`) | Checkers and Reversi |
| `qlink-casino.d64` | RabbitJack's Casino (`DATA`) | the casino lounge and its games |
| `qlink-superq.d64` | Super-Q (`WIMEDATA`) | Super-Q rooms |
| `club-caribe-side1.d64` | Club Caribe program disk (`CLUB CARIBE`) | Club Caribe / Habitat |
| `club-caribe-side2.d64` | Club Caribe image disk (`HABITAT DATA`) | Club Caribe / Habitat (stays in the drive) |

## Getting started
1. Make **your own working copies** of the images and keep these downloads untouched as a backup. The client writes
   your registration to its disk, and the Club Caribe image disk is updated by the server when you enter, so the
   working copies must be **writable**. Never share your working client disk: it holds your account details.
2. Point your modem (or modem emulator) at `qlink.kd4cbm.us`, port `5190`.
3. Boot the client: `LOAD"*",8,1`. New members register from the client; it saves your account to the disk.
4. When Q-Link asks for another disk (games, casino, Super-Q, Club Caribe), insert the matching image and follow the prompt.
   Club Caribe asks for side 1 first, then the image disk (side 2), which stays in the drive while you play.
5. Club Caribe controls: joystick in **port 1**; fire + up / down / right / left = GO / DO / GET / PUT; F1 = ghost.

## What is different from other copies
- **`qlink-client-v4.d64`**: the 2005 archive copy with its user block (track 18, sector 15) reset to the factory-blank
  state. The archive copy still held an old registration; nothing else on the disk is changed.
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
