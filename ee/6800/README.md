- [README](README.md), [asm](asm.md), [opcodes](opcodes.md),
  [progcard](progcard)

Motorola 6800-series Microprocessors and Microcontrollers
=========================================================

This covers the Motorola 6800 series processors ([timeline]):
- __6800__ (1974-11): 1 MHz. External clock required.
  __68A00__=1.5 MHz, __68B00__=2.0 MHz (1976).
- [README](README.md), [asm](asm.md), [opcodes](opcodes.md),
  [progcard](progcard)

- __6802__, __6808__ (1977-03): Internal clock. '02 has 128 bytes of RAM
  (because the 6846 has no RAM) and can preserve 32 bytes of it with
  standby power.
- __6801__, __6803__ (1978-08): (Used by GMC.) [asm](asm.md) for details.
  - Architecture: D register; PHX, multiply and other
  - Hardware: 128 B RAM, 16-bit timer, UART, up to 13 PIA lines.
  - 6801 has up to 31 PIA lines, 2 KB mask ROM.

Hitachi equivalents:
- __HD6801__: NMOS TTL; compat MC6801. S has 2K (?) ROM; V0,V5 have 4K.
  V0 1 MHz; V5 1.25 Mhz.
- __HD6301__: CMOS TTL (except some pins); up.compat HD6801.
  - Series uses nothing/A/B/C in middle for 1.0/1.5/2.0/3.0 Mhz.
  - Suffix after V1/X0/Y0/etc: P=DIP, F=QFP, CP=different QFP
  - Suffix V1: DIP-40; 128b RAM, 4k ROM
  - Suffix X0: DIP-64; 192b RAM, 4k ROM
  - Suffix Y0: DIP-64; 256b RAM, 16k ROM

This does not cover:
- __6805__ (1979): 8-bit X register and other incompatible changes.
  M14065: CMOS version. 68HC05: low power version. 6804: reduced cost
  version.
- __6811__ (1984): Greatly extended 6801. Available in modern versions.
- __6809__ (1979-07): Entirely incompatible.

### Peripherals

- __6820, 6821:__ [Peripheral Interface Adapter (PIA)](../mc6820.md).
- __[6845]__ CRT Controller (CRTC). Interface beteween MPU/memory and
  raster-scan waveform generator. Very flexible.
- __[6846]__ ROM – I/O – Timer
- __[6847]__ Video Display Generator (VDG). Used in CoCo, etc.
- __[6850]__ Asynchronous Communications Interface Adapter (ACIA).
- __[6852]__ Synchronous Serial Data Adapter (SSDA)
- __[6854]__ Advanced Data-Link Controller (ADLC). Supports ADCCP (Advanced
  Data Comunication Control Procedure), HDLC, SDLC. Used for Acorn's
  Econet. Includes features such as zero insertion/deletion and abort/idle
  detection/transmition.


References
----------

- \[PRM] [M6800 Programming Reference Manual][PRM] M68PRM(D).
  Motorola, Nov. 1976.
- [SB-Project 6800 Introduction][sb 6800intro]. Brief programming model
  introduction and SB-Assembler support for the 6800/6802.


Bibliography
------------

- \[mikrom] Mike Wiles, [_MCM6830L7 MIKBUG/MINIBUG ROM_][mikrom]. Motorola,
  1977.
  - Usage instructions and assembly listing.
  - $E000-$E1FF MIKBUG v9. $A000-$A043 RAM. $8004-$8007 PIA (bit-bang serial).
  - $FE00-$FEFF MINIBUG v4. $FF00-$FF36 RAM. $FCF4-$FCF5 ACIA control/status.
  - 1024-byte ROM contained, low to high: MIKBUG, MINIBUG, test pattern.
  - "Restart address generator" required for $FFFE word.

  RAM @$A000. Bit-bangs serial IO via 6820 PIA @$8004.
- \[fin76] Robert Findley, [_6800 Software Gourment Guide and
  Coookbook_][fin76]. Hayden, 1976.
  - Very much a beginners' book. Ch.5 floating point routines might be of
    some interest. Written by Scelbi staff.

There's a [very large bibliography][og bib] at orphanedgames.com.



<!-------------------------------------------------------------------->
[timeline]: https://retrocomputing.stackexchange.com/a/11933/7208
[6845]: https://archive.org/details/bitsavers_motoroladaMicroprocessorsDataManual_80083566/page/n525/mode/1up
[6846]: https://archive.org/details/bitsavers_motoroladaMicroprocessorsDataManual_80083566/page/n548/mode/1up
[6847]: https://archive.org/details/bitsavers_motoroladaMicroprocessorsDataManual_80083566/page/n568/mode/1up
[6850]: https://archive.org/details/bitsavers_motoroladaMicroprocessorsDataManual_80083566/page/n595/mode/1up
[6852]: https://archive.org/details/bitsavers_motoroladaMicroprocessorsDataManual_80083566/page/n604/mode/1up
[6854]: https://archive.org/details/bitsavers_motoroladaMicroprocessorsDataManual_80083566/page/n618/mode/1up

<!-- References -->
[PRM]: https://archive.org/stream/bitsavers_motorola68rammingReferenceManualM68PRMDNov76_6944968#page/n0/mode/1up
[sb 6800intro]: https://www.sbprojects.com/sbasm/6800.php

<!-- Bibliography -->
[fin76]: https://archive.org/stream/6800-Software-Gourmet-Guide-and-Cookbook-Robert-Findley-1976#page/n0/mode/1up
[mikrom]: https://archive.org/stream/bitsavers_motorola680MCM6830L7MIKBUGMINBUGROMJul77_1952205#page/n0/mode/1up
[og bib]: https://www.orphanedgames.com/APF/6800_cpu_programming/6800_cpu_programming.html
