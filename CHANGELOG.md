# Changelog

All notable changes to these disk images. Newest first. Versions follow [Semantic Versioning](https://semver.org/):
public releases are `vMAJOR.MINOR.PATCH`, with `-beta.N` for pre-releases. Every version is a git tag; public versions also have
a GitHub Release with the images and checksums.

## [Unreleased]
- New: **`vice/`**, the Public Release Beta 1 D81 for the VICE emulator (`qlink-ultimate-vice.d81`, manual dial: press F1 at the
  modem screen) and its pre-filled 2 MB REU image (`qlink-ultimate-vice-2mb.reu`), with the VICE settings in `vice/README.md`.
  Same build and set stamp as `v1.0.0-beta.1` (`QLULT-24cf9da76`); only the dial setting differs from the Ultimate image.
- Release page of `v1.0.0-beta.1` (no change to the tagged files): it now also carries the user-port set as one zip
  (`kd4cbm-qlink-disks-userport-v1.0.0-beta.1.zip`: the seven D64s at the tag, `CONNECTING.md`, the Member's Guide, the
  checksums) and is the **Latest** release, so the releases page leads every C64 to the current disks. The old `v1` release
  (2026-10-19 set, before the main-menu freeze fix) stays as it was, marked superseded.

## [v1.0.0-beta.1] - 2026-10-23 - Public Release Beta 1
The first public release. For the Commodore 64 Ultimate: one D81 image with everything.
### Added
- **Super-Q on the Ultimate D81**: hold C= and press F1 on People Connection; the main menu says `C=+F1: Super-Q`. Super-Q's
  Return to Q-Link comes back to the main menu.
### Changed
- `ultimate/qlink-ultimate-swiftlink-de00.d81` (and its optional `-16mb.reu`) is now **the** Ultimate image: the client, both game
  disks, RabbitJack's Casino, Club Caribe and Super-Q, no disk swaps. The per-disk SwiftLink images of the tester betas stay in
  `ultimate/` for testers; the user-port set is unchanged.
### Known issues
- After Super-Q > Return to Q-Link, the main menu does not show the `C=+F1: Super-Q` line (C= + F1 still works).

Built from the KD4CBM build tree `dev/reu-store` at `24cf9da` (set stamp `QLULT-24cf9da76`).

## Tester betas (before the public release)
These were for the beta testers. Each is a tag (`tester-beta.N`); the images of each are in that tag.

### tester-beta.6 - 2026-10-23 (`56a5263`)
- New: `ultimate/qlink-ultimate-swiftlink-de00.d81`, the client, both game disks, RabbitJack's Casino and Club Caribe (both sides)
  on one 1581 image with the REU store; Club Caribe's fast disk code ported to the 1581. Optional
  `ultimate/qlink-ultimate-swiftlink-de00-16mb.reu` (pre-filled REU store for REU Size 16 MB).

### tester-beta.5 - 2026-10-21 (`96b4abd`)
- Club Caribe side 1 works on the real C64 Ultimate (polled send; a 1986 sequence-number bug fixed). Quit key is SHIFT + RUN/STOP.

### tester-beta.4 - 2026-10-21 (`0b6a2a0`)
- Club Caribe side 1: a dropped connection no longer freezes it on leaving ("Connection lost." after about 50 seconds).

### tester-beta.3 - 2026-10-20 (`4369807`)
- New: Club Caribe side 1 for the SwiftLink. Client and casino: two latent raster fixes.

### tester-beta.2 - 2026-10-20 (`8e04c76`)
- Clients: fix for the random freeze at the main menu after sign-on.

### tester-beta.1 - 2026-10-20 (`3c46119`)
- New: `ultimate/`, disks for the Ultimate's SwiftLink-type modem interface (ACIA at `$DE00`) with a pre-configured client.

### v1 - 2026-10-19 (`d4bfbf1`)
- The first tester disk set: the original user-port disks (client, games, casino, Super-Q, Club Caribe), sanitized. This tag
  predates the version scheme above; it is kept as it is.
