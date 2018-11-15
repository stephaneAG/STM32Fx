### R: stuff to digg to make that damn board work ? hopefully ..

- related troubles on Espruino forums ? ( at least, the guy has a /dev/tty*** poping up ;p ) http://forum.espruino.com/conversations/1250/
- related board that works ? https://www.ebay.fr/itm/STM32-STM32F407VET6-Core407V-Cortex-M4-Development-Board-Mainboard-Module-FR/173483164116?_trkparms=aid%3D777003%26algo%3DDISCL.MBE%26ao%3D1%26asc%3D20140620091512%26meid%3D067b617565a14be4947fbf7c76317dcd%26pid%3D100009%26rk%3D6%26rkt%3D10%26sd%3D263106386751%26itm%3D173483164116&_trksid=p2047675.c100009.m1982
- actual board that doesn't allows flashing ?! https://www.ebay.fr/itm/STM32F103C8T6-F407VET6-STM32F407VGT6-ARM-Cortex-M4-32bit-Core-Development-Board/263517220225?var=562547481663&_trkparms=aid%3D222007%26algo%3DSIM.MBE%26ao%3D1%26asc%3D20170920101122%26meid%3Db24c7cba96484397bfdfe9d7ec8dba64%26pid%3D100010%26rk%3D1%26rkt%3D12%26sd%3D263106386751%26itm%3D562547481663&_trksid=p2047675.c100010.m2109
- this guy got it right ? https://www.instructables.com/id/Upload-Arduino-Sketch-to-STM32F407-Board/
- some right infos .. but I couldn't get flash to work .. https://edoc.site/diy-more-stm32f407vgt6-boar1-pdf-free.html
- schematic showing BOTT0 & BOTT1 among others .. http://dubstylee.net/v/wp-content/uploads/2017/08/DIY-More-STM32F407VGT6.png
- reference ( corresponding discovery board ):  http://www.espruino.com/ReferenceSTM32F4DISCOVERY
- serial bootloading: http://www.espruino.com/Serial+Bootloader
- advanced debug: http://www.espruino.com/AdvancedDebug
- some hints ? http://hightechdoc.net/mecrisp-stellaris/_build/html/terminal-connections.html#serial-connections
- TO TRY MAYBE ?? http://blog.davehylands.com/2014/02/serial-bootloading-stm32f4.html
- USB to serial on F103xx https://www.youtube.com/watch?v=G_RF0a0hrak
- stm32loader.py https://pypi.org/project/stm32loader/
- user manual for corresponding discovery board: https://www.st.com/content/ccc/resource/technical/document/user_manual/70/fe/4a/3f/e7/e1/4f/7d/DM00039084.pdf/files/DM00039084.pdf/jcr:content/translations/en.DM00039084.pdf
- windaube STL-LINK "can't connect": https://www.youtube.com/watch?v=jEz0C2bT2M0
- JTAG/SWD debug on "blue pills" stm32F103xx https://satoshinm.github.io/blog/171223_jtagswdpillblink_jtagswd_debugging_via_black_magic_probe_on_an_stm32_blue_pill_and_blinking_a_led_using_stm32cubemx_libopencm3_and_bare_metal_c.html
- EEVBlog guy talks on stm32f chips https://www.youtube.com/watch?v=mkx4qZCCHqI

### Reminders:
To flash stuff using smt32loader.py
```
python stm32loader.py -p /dev/tty.usbserial-A50285BI -ew -V -b 57600 ./espruino_1v92.3_stm32f4discovery.bin
```

To get infos on the chip using st-info ( part of st-link cli tools ):
```
./build/Release/st-info --chipid
```

To flash stuff using st-flash ( part of st-link cli tools ):
```
./build/Release/st-flash write ./espruino_1v92/espruino_1v92.3_stm32f4discovery.bin 0x08000000
```

### some doc from which I wrote my pinout ;)
- jap & code :http://dubstylee.net/v/stm32duino-bootloader-build/
- same as above for board: http://dubstylee.net/v/diy-more-stm32f407vgt6/
- some nteresting infos & fixes : https://github.com/rogerclarkmelbourne/STM32duino-bootloader/
- getting the USB to work: https://www.stm32duino.com/viewtopic.php?f=39&t=2666&sid=7f3725152715d8b2c79fa030bb125d51&start=10
- VET6 version of the schematic: http://wiki.stm32duino.com/images/6/69/Vcc-gnd.com-STM32F407VET_mini-schematic.pdf
- partial & non-that-intelligible translation of jap + code board page: https://edoc.site/diy-more-stm32f407vgt6-boar1-pdf-free.html
- 

### Getting everything working on it ;)
- STM32F407VGT6 breakout board baremetal examples: https://github.com/dwelch67/black_pill_too
- Working way to flash the board :D : http://stm32f4-discovery.net/2014/09/program-stm32f4-with-uart/

### getting backups & DFU stuf
- http://alain.wanamoon.net/2014/06/28/restoring-original-flash-contents-to-the-stm32f4-discovery/
- http://oshgarage.com/dfu-mode-on-a-stm32-microcontroller/

### TO DIGG ( libs & features offered by the SMT32 & tutorials )
- all ST lib: http://stm32f4-discovery.net/2015/07/all-stm32-hal-libraries/
- USB libs: http://stm32f4-discovery.net/2015/08/hal-library-21-multi-purpose-usb-library-for-stm32fxxx/
- some links: http://stm32f4-discovery.net/stm32f4-links/
- lots of tuts: http://stm32f4-discovery.net/category/stm32f4-2/
- https://github.com/rowol/stm32_discovery_arm_gcc/tree/master/usb_cdc_vcp

### On USB HOST + DEVICE combo ( for MitM passhrough & Xbox360 controller hack ;p )
- https://community.st.com/s/question/0D50X00009Xkaw6SAB/hid-usb-host-example-ported-to-stm32f4-discovery-mouse-keyboard
- https://www.st.com/en/embedded-software/stsw-stm32046.html
- actual doc: https://www.st.com/content/ccc/resource/technical/document/user_manual/1c/6b/06/e6/19/6c/46/bf/CD00289278.pdf/files/CD00289278.pdf/jcr:content/translations/en.CD00289278.pdf
- example from a wise individual: http://moretosprojects.blogspot.com/2014/12/stm32f4-usb-host-and-device.html
- schematic for the above example ( note the 10k for the USB acting as HOST .. ): http://3.bp.blogspot.com/-b1dRjJKVorE/VH9OHlCAAeI/AAAAAAAAIeg/8-2qKZ0f8u8/s1600/STM32F4_usb_sch.png
