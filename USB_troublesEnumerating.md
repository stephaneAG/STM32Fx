R:  
The STM32F407VGT6 "diyMrOE" board has troubles appearing to a alptop as USB VCP for firmwares handling it ( Ex: Espruino )  
Adding a 1.5k resistor tying between PA12 & Vcc seems to work on Windaube, but for me doesn't on Mac OS X :/

The following links may help fix this torubles ..
- bluepill won't enumerate: http://stm32duino.com/viewtopic.php?f=3&t=2922
- bootloader, a pin for the D+ DISCconnect: http://www.stm32duino.com/viewtopic.php?f=32&t=1307&start=20
- bluepill with disconnect circuit added: http://www.stm32duino.com/viewtopic.php?t=780
- redpill or bluepill: http://stm32duino.com/viewtopic.php?f=28&t=117
