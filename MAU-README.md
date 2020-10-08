pio lib install "U8glib"
vim platformio.ini

#
# ATmega2560
#
[env:mega2560]
framework = arduino
platform            = atmelavr
extends             = common_avr8
board               = megaatmega2560

platformio run -e mega2560 --target upload
pio -f -c atom serialports monitor --raw --port /dev/ttyUSB0 -b 250000

