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
