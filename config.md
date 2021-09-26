# voron-switchwire

### Setup and config voron switchwire on SKR Mini E3 V1.2

MainsailOS or FluiddPi or Octoprint


![image](https://user-images.githubusercontent.com/38026441/134792005-bcf636cd-efd6-4438-a860-19235d42c0d4.png)


### Step 1: 

git clone https://github.com/Klipper3d/klipper

./klipper/scripts/install-octopi.sh

### Step 2:

cd ~/klipper/

make menuconfig


![image](https://user-images.githubusercontent.com/38026441/134791939-5e5be692-403c-4123-9cba-58fd82cee722.png)



```wrap

pi@octopi:~/klipper $ make clean
pi@octopi:~/klipper $ make
  Creating symbolic link out/board
  Building out/autoconf.h
  Compiling out/src/sched.o
  Compiling out/src/command.o
  Compiling out/src/basecmd.o
  Compiling out/src/debugcmds.o
  Compiling out/src/initial_pins.o
  Compiling out/src/gpiocmds.o
  Compiling out/src/stepper.o
  Compiling out/src/endstop.o
  Compiling out/src/trsync.o
  Compiling out/src/adccmds.o
  Compiling out/src/spicmds.o
  Compiling out/src/thermocouple.o
  Compiling out/src/i2ccmds.o
  Compiling out/src/pwmcmds.o
  Compiling out/src/spi_software.o
  Compiling out/src/sensor_adxl345.o
  Compiling out/src/lcd_st7920.o
  Compiling out/src/lcd_hd44780.o
  Compiling out/src/buttons.o
  Compiling out/src/tmcuart.o
  Compiling out/src/neopixel.o
  Compiling out/src/pulse_counter.o
  Compiling out/src/stm32/watchdog.o
  Compiling out/src/stm32/gpio.o
  Compiling out/src/generic/crc16_ccitt.o
  Compiling out/src/generic/armcm_boot.o
  Compiling out/src/generic/armcm_irq.o
  Compiling out/src/generic/armcm_reset.o
  Compiling out/src/../lib/stm32f1/system_stm32f1xx.o
  Compiling out/src/stm32/stm32f1.o
  Compiling out/src/generic/armcm_timer.o
  Compiling out/src/stm32/adc.o
  Compiling out/src/stm32/i2c.o
  Compiling out/src/stm32/spi.o
  Compiling out/src/stm32/usbfs.o
  Compiling out/src/stm32/chipid.o
  Compiling out/src/generic/usb_cdc.o
  Compiling out/src/stm32/hard_pwm.o
  Building out/compile_time_request.o
Version: v0.9.1-659-g69d9497d
  Preprocessing out/src/generic/armcm_link.ld
  Linking out/klipper.elf
  Creating hex file out/klipper.bin
pi@octopi:~/klipper $

```
