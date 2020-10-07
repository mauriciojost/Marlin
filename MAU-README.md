

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



./buildroot/tests/run_tests . mega2560

