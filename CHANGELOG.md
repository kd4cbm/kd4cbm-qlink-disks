# Changelog

All notable changes to these disk images. Newest first. Versions follow [Semantic Versioning](https://semver.org/):
public releases are `vMAJOR.MINOR.PATCH`, with `-beta.N` for pre-releases. Every version is a git tag; public versions also have
a GitHub Release with the images and checksums.

## [Unreleased]
- Public Release Beta 1 (`v1.0.0-beta.1`) in preparation: the single-disk D81 for the Commodore 64 Ultimate with Club Caribe and
  Super-Q (hold C= when choosing People Connection).

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
