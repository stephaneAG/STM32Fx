# STM32Fx
Repo dedicated to the STM32Fx boards

### hacking around with those:
- https://media.defcon.org/DEF%20CON%2025/DEF%20CON%2025%20presentations/DEFCON-25-skud-and-Sky-If-You-Give-A-Mouse-A-Microchip-UPDATED.pdf
- https://www.youtube.com/watch?v=r4XntiyXMnA --> DEF CON 24 Internet of Things Village - Elvis Collado - Reversing and Exploiting Embedded Devices

### digg the following repo for a lot of topics related to those
- https://github.com/stephaneAG/OpenAdaptiveController

### installing the necessary, compiling & flashing
- https://www.davidyamnitsky.com/blog/2013/11/14/stm32-mac

StephaneAG nb: no .bin found for Espruino 1V99 on STM32F3discovery, digging helped find the followings
at http://www.espruino.com/binaries/travis/0aa0a8aefb9a3c6f63c9453a2f531613be28d01e/ & then www.espruino.com/files/espruino_1vxx.zip

R: visit http://www.espruino.com/ReferenceSTM32F3DISCOVERY
R: stm32f3discovery -> 'USB BROKEN', so trying a version <1V8 to test until able to fix it or find a fix ..

espruino_1v92_stm32f3discovery.bin,
espruino_1v92.3_stm32f3discovery.bin
   - STM32F3DISCOVERY board
   
NOTES:

On the STM32F3DISCOVERY:
Plug in to the port labelled 'USB USER'. Note: This board is more difficult to connect to. You need to power up the board without 'USB USER' plugged in, and then plug in USB later. If you subsequently reset the board, you'll need to unplug USB and plug it back in.

* On the STM32F4DISCOVERY the default USART is USART2 (because
USART1 shares some pins with USB). This means you must connect
serial connections to PA2/PA3 NOT PA9/PA10 as you would for
the STM32VLDISCOVERY.


==== Tef tut from espruino.com/Other-Boards > STM32F3DISCOVERY ====

==
Infos when connecting both USB plugs ( default firmware ! )
==
STM32 STLink :

  Identifiant du produit :	0x3748
  Identifiant du fournisseur :	0x0483  (STMicroelectronics)
  Version :	1.00
  Numéro de série :	Wÿm?guTUFX?g
  Vitesse :	Jusqu’à 12 Mb/s
  Fabricant :	STMicroelectronics
  Identifiant de l’emplacement :	0xfa130000 / 5
  Courant disponible (mA) :	500
  Courant requis (mA) :	100
  Exploitation supplémentaire actuelle (mA) :	0
==
STM32 Joystick :

  Identifiant du produit :	0x5710
  Identifiant du fournisseur :	0x0483  (STMicroelectronics)
  Version :	2.00
  Numéro de série :	3DC2748AFFFF
  Vitesse :	Jusqu’à 12 Mb/s
  Fabricant :	STMicroelectronics
  Identifiant de l’emplacement :	0xfd120000 / 3
  Courant disponible (mA) :	500
  Courant requis (mA) :	100
  Exploitation supplémentaire actuelle (mA) :	0


Flashing:
    brew install libusb  
    git clone https://github.com/texane/stlink.git  
    cd stlink  
    LIBRARY_PATH=/usr/local/lib  
    C_INCLUDE_PATH=/usr/local/include  
    #./autogen.sh  
    #./configure  
    make

Extract the archive containing Espruino to the stlink directory.
Go to the stlink directory, and type: 'flash/st-flash write espruino_1vXX<boardModel>.bin 0x08000000'

==
Ex: ./build/Release/st-flash write ./espruino_1v92/espruino_1v92.3_stm32f3discovery.bin 0x08000000s
== the above gives the following ( when plugging in both usb plugs, 1st 'USB-ST-LINK', then 'USB-USER')
st-flash 1.4.0-50-g7fafee2
2018-10-07T01:45:27 INFO usb.c: -- exit_dfu_mode
2018-10-07T01:45:27 INFO common.c: Loading device parameters....
2018-10-07T01:45:27 INFO common.c: Device connected is: F3 device, id 0x10036422
2018-10-07T01:45:27 INFO common.c: SRAM size: 0xa000 bytes (40 KiB), Flash: 0x40000 bytes (256 KiB) in pages of 2048 bytes
2018-10-07T01:45:27 INFO common.c: Attempting to write 203936 (0x31ca0) bytes to stm32 address: 134217728 (0x8000000)
Flash page at addr: 0x08031800 erased
2018-10-07T01:45:30 INFO common.c: Finished erasing 100 pages of 2048 (0x800) bytes
2018-10-07T01:45:30 INFO common.c: Starting Flash write for VL/F0/F3/F1_XL core id
2018-10-07T01:45:30 INFO flash_loader.c: Successfully loaded flash loader in sram
100/100 pages written
2018-10-07T01:45:41 INFO common.c: Starting verification of write complete
2018-10-07T01:45:45 INFO common.c: Flash written and verified! jolly good!
== trying with firmware < 1V8
./build/Release/st-flash write ./espruino_1v92/espruino_1v87.349_stm32f3discovery.bin 0x08000000



== R: default firmware location: /Users/philippegarnier/STM32Cube/Repository/STM32Cube_FW_F3_V1.10.0

== trying to recover the default app: 
// did NOT work:
./build/Release/st-flash write /Users/philippegarnier/STM32Cube/Repository/STM32Cube_FW_F3_V1.10.0/Projects/STM32F3-Discovery/Demonstrations/Binary/STM32CubeF3_Demo_STM32F3-DISCOVERY.hex 0x08000000
// DID work :)
./build/Release/st-flash erase
./build/Release/st-flash --format ihex write /Users/philippegarnier/STM32Cube/Repository/STM32Cube_FW_F3_V1.10.0/Projects/STM32F3-Discovery/Demonstrations/Binary/STM32CubeF3_Demo_STM32F3-DISCOVERY.hex

== trying to get the needed stuff to compile things :D
# getting 2 homebrew formulas to get components needed to compile& run code
brew tap nitsky/stm32
# install gcc compiler for ARM
brew install arm-none-eabi-gcc
# install stlink ( to manage connections to the ST-LNK JTAG programmer )
brew install --HEAD stlink # couldn"t get it to work
# tried
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
# worked ?
brew install stlink # aka won't be the cutting edge vers ?

== retying to get a "basic" HID example working ( acting as a mouse )
- 1st: generate stuff using STM32CubeMX
- 2nd: mod main.c to add stuff within 'USER CODE BEGIN 1' & 'USER CODE BEGIN 3'
- 3rd: run 'make' from the generated project directory
- 4th: flash the board with the generated hex & pray ? .. IT WORKED ( aka mac os x sys infos reported an STM32 HID & my mouse pointer was going to the right every second ;P ) !!! ( also, I don't know yet how to use gdb & stlink .. )
./build/Release/st-flash --format ihex write ./../MyProjects/stm32f3discovery_hidTest1/build/stm32f3discovery_hidTest1.hex
