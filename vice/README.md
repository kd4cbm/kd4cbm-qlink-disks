# Q-Link in VICE: the single D81 image

The Ultimate's one-image disk set for the **VICE** emulator: the Q-Link client, both People Connection games disks,
RabbitJack's Casino, Club Caribe and Super-Q on one 1581 image, with the REU store, no disk swaps. It is the
Public Release Beta 1 build (`v1.0.0-beta.1`, set stamp `QLULT-24cf9da76`); the only difference from
[`ultimate/qlink-ultimate-swiftlink-de00.d81`](../ultimate/) is the dial setting: VICE has no Hayes modem, so this client is
**manual dial** (you press F1 at the modem screen) and VICE connects the emulated SwiftLink straight to the server.

| File | What it is |
|---|---|
| `qlink-ultimate-vice.d81` | the image (no account on it: the first sign-on makes yours) |
| `qlink-ultimate-vice-2mb.reu` | Q-Link's REU store, already filled, for a **2 MB** REU (optional, but the first start is much faster with it) |

## VICE settings
Tested with VICE 3.10 (x64sc). Command line (Windows; on macOS/Linux the same options):

```
x64sc -drive8type 1581 -drive8truedrive -reu -reusize 2048 -reuimage qlink.reu -reuimagerw
      -userportdevice 0 -acia1 -acia1mode 1 -acia1base 0xDE00 -acia1irq 1 -myaciadev 2
      -rsdev3 qlink.kd4cbm.us:5190 +rsdev3ip232 qlink.d81
```

The same in VICE's settings dialog:

| Setting | Value |
|---|---|
| Drive 8 | **1581**, true drive emulation on |
| REU (RAM Expansion Module) | **enabled, 2048 KB**, image `qlink.reu`, written back on exit |
| ACIA | **SwiftLink** at **$DE00**, interrupt **NMI**, connected to **RS232 device 3** |
| RS232 device 3 | `qlink.kd4cbm.us:5190`, **IP232 off** (a raw connection) |
| User port | no device (no user-port modem) |
| KERNAL | the standard one (**not JiffyDOS**) |

## Start
1. Copy both files to a folder of your own and rename them `qlink.d81` and `qlink.reu` (keep the originals: your copies get
   written to). The D81 must be **writable**: your account is saved on it at the first sign-on.
2. Start VICE as above and type `LOAD"QUANTUM",8,1` (RETURN). With the REU image it says "Q-Link uses the whole REU (2 MB)."
   and comes to the modem screen in about 20 seconds.
3. At "Type commands to the modem, then press F1 when connection is made." **press F1 without typing anything**.
4. First visit: pick a screen name and answer four questions. Next time the same D81 signs you straight on.
5. **Super-Q:** hold C= and press F1 on People Connection (the main menu says `C=+F1: Super-Q`). **Club Caribe:** People
   Connection > F7 > Play or observe an online game > Start a game > Club Caribe; SHIFT + RUN/STOP (VICE: SHIFT + Esc) to leave.

Without the REU image VICE still works (REU enabled, 2 MB): Q-Link sets up an empty store, the first start takes about a minute
longer, and each area loads from the disk on your first visit.

## Known issues
* After **Super-Q > Return to Q-Link**, the main menu does not show the `C=+F1: Super-Q` line (C= + F1 still works). Fixed in
  the next beta.

Prefer the classic disks or a user-port modem in VICE? The 1541 `.d64` set at the top of this repository works with VICE's
user-port RS-232 too; see [CONNECTING.md](../CONNECTING.md).
