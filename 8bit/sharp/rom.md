Sharp MZ-series ROM
===================

ROM contains only IPL support, a small monitor, and enough BIOS code to
support these.

All values are in hex.


Keyboard and Screen Information
-------------------------------

Special key codes returned by `GETKY` etc.:

      Key Code Screen Code      Key Code Screen Code
      DEL  60    C7               ↓  11    C1
     INST  61    C8               ↑  12    C2
    ALPHA  62    C9               →  13    C3
    BREAK  64    CB               ←  14    C4
       CR  66    CD            HOME  15    C5
                                CLR  16    C6


ROM Memory, Variables and Subroutines
-------------------------------------

### Memory Map

    1200   free for user use
    11A3   key input buffer
    1170   variable area
    10F0   CMT header area
    10EF   start of stack (initial SP set to $10F0)
    1000   stack area
    0000   ROM; monitor code

### Variables

Variable locations (all values in hex): [[smzo-monicmd]]

    addr  len   name    descr
    10F0   80   IBUFE   tape header buffer
    103C   B4   SP      180 bytes for stack
    1038    3           jp to time interrupt (038D)
    1000   38           unused

### BIOS API (Jump Table)

Standard routines (subscript is RST number) [[som 151]]:

    0000 ₀  MONIT   monitor on (reset entry point)
    0003    GETL    ♡全 get line ending in CR or shift-break; DE→input buf
                        max 80 chars, echos chars, break/CR codes included
    0006    LETNL   ♣A cursor to beginning of next line
    0009    NL
    000C    PRNTS   ♣A print space
    000F    PRNTT   print tab
    0012    PRNT    print 1 character
    0015    MSG     ♡全 print message ♠DE→msg, end w/CR (not printed)
                        control codes 11-16 move cursor
    0018 ₃  MSGX
    001B    GETKY   ♣A get keycode in A, or $00 = no key pressed
    001E    BRKEY   ♣A z=1 if shift+break being pressed, z=0 otherwise
    0021    WRINF   write information (tape header?)
    0024    WRDAT   write data (tape data?)
    0027    RDINF
    002A    RDDAT
    002D    VERFY   verify CMT (header and?) data
    0030 ₆  MELDY   ♣A play music DE→music data (same format as BASIC)
                        end w/CR or $C8. cy=0 no break, cy=1 break intr.
    0033    TIMST   ♣A set time ACC=0(AM),1(PM), DE=time in secs
    0038            interrupt routine (jp $1038)
    003B    TIMRD   ♠A,DE read time (per TIMST)
    003E    BELL    ♣A briefly sound ~880 Hz
    0041    XTEMP   ♡全 tempo set (A=tempo, 0=slowest, 7=highest)
    0044    MSTA    melody start
    0047    MSTP    ♣A melody stop

### Internal Routines

These are described in the user's manual, so are presumably unlikely to
change location. [[som 151]]

    03DA  ASC     ♠A ← ASCII char for number in A low nybble
    03F9  HEX     ♠A ← number represented by ASCII value in A
    0410  HLHEX   ♣A ♠HL ← 16-bit value repres. by DE → 4 ASCII chars
                      cy 0=success, 1=fail
    041F  2HEX    ♣DE ♠A -< 8-bit vlaue repres. by DE → 2 ASCII chars
    09B3  ??KEY   ♠A blink cursor, wait for keypress, code returned in A
    0BB9  ?ADCN   ♠A ← display code from ASCII code in A
    0BCE  ?DACN   ♠A ← ASCII code from display code in A
    0DA6  ?BLNK   ♡全 wait for vertical blank period to start
    0DDC  ?DPCT   ♡全 "display control": A=screen code for key to emulate (↑)
    0FB1  ?PONT   ♣A ♠HL ← current cursor location


Hardware Modification
---------------------

### ROM Replacement

European/PAL ROMs may be different from the Japanese ones.

- MZ-80K:  The IPL/Monitor ROM is in a 2332 (4K×8). This can be replaced
  with a 2532 without modification, or a 2732 by grounding pin 18,
  connecting the track for 18 to 21, and cutting the existing pin 21 track.
  [[smzo-h&t]]
- MZ-700: uses a 2732.



<!-------------------------------------------------------------------->
[smzo-h&t]: https://original.sharpmz.org/mz-80k/tips.htm
[smzo-monicmd]: https://original.sharpmz.org/mz-700/monicmd.htm
[som 151]: https://archive.org/details/sharpmz700ownersmanual/page/n153/mode/1up?view=theater
