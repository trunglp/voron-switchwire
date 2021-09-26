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


Chú ý: 

SKR mini E3 V1.2 => pin !PC13
SKR mini E3 V2.0 => pin !PC14


### Step 3: build firmware

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

### Check my config

```wrap

pi@octopi:~/klipper $ cat .config
CONFIG_LOW_LEVEL_OPTIONS=y
# CONFIG_MACH_AVR is not set
# CONFIG_MACH_ATSAM is not set
# CONFIG_MACH_ATSAMD is not set
# CONFIG_MACH_LPC176X is not set
CONFIG_MACH_STM32=y
# CONFIG_MACH_RP2040 is not set
# CONFIG_MACH_PRU is not set
# CONFIG_MACH_LINUX is not set
# CONFIG_MACH_SIMU is not set
CONFIG_STEP_DELAY=2
CONFIG_BOARD_DIRECTORY="stm32"
CONFIG_MCU="stm32f103xe"
CONFIG_CLOCK_FREQ=72000000
CONFIG_USBSERIAL=y
CONFIG_FLASH_START=0x8007000
CONFIG_FLASH_SIZE=0x10000
CONFIG_RAM_START=0x20000000
CONFIG_RAM_SIZE=0x5000
CONFIG_STACK_SIZE=512
CONFIG_STM32_SELECT=y
CONFIG_MACH_STM32F103=y
# CONFIG_MACH_STM32F207 is not set
# CONFIG_MACH_STM32F401 is not set
# CONFIG_MACH_STM32F405 is not set
# CONFIG_MACH_STM32F407 is not set
# CONFIG_MACH_STM32F429 is not set
# CONFIG_MACH_STM32F446 is not set
# CONFIG_MACH_STM32F031 is not set
# CONFIG_MACH_STM32F042 is not set
# CONFIG_MACH_STM32F070 is not set
# CONFIG_MACH_STM32F072 is not set
CONFIG_MACH_STM32F1=y
CONFIG_HAVE_STM32_USBFS=y
CONFIG_HAVE_STM32_CANBUS=y
# CONFIG_STM32_FLASH_START_2000 is not set
# CONFIG_STM32_FLASH_START_5000 is not set
CONFIG_STM32_FLASH_START_7000=y
# CONFIG_STM32_FLASH_START_8800 is not set
# CONFIG_STM32_FLASH_START_10000 is not set
# CONFIG_STM32_FLASH_START_800 is not set
# CONFIG_STM32_FLASH_START_4000 is not set
# CONFIG_STM32_FLASH_START_0000 is not set
CONFIG_STM32_CLOCK_REF_8M=y
# CONFIG_STM32_CLOCK_REF_12M is not set
# CONFIG_STM32_CLOCK_REF_16M is not set
# CONFIG_STM32_CLOCK_REF_25M is not set
# CONFIG_STM32_CLOCK_REF_INTERNAL is not set
CONFIG_CLOCK_REF_FREQ=8000000
CONFIG_STM32F0_TRIM=16
CONFIG_STM32_USB_PA11_PA12=y
# CONFIG_STM32_SERIAL_USART1 is not set
# CONFIG_STM32_SERIAL_USART1_ALT_PB7_PB6 is not set
# CONFIG_STM32_SERIAL_USART2 is not set
# CONFIG_STM32_SERIAL_USART2_ALT_PD6_PD5 is not set
# CONFIG_STM32_SERIAL_USART3 is not set
# CONFIG_STM32_SERIAL_USART3_ALT_PD9_PD8 is not set
# CONFIG_STM32_CANBUS_PA11_PA12 is not set
# CONFIG_STM32_CANBUS_PB8_PB9 is not set
CONFIG_CANBUS_FREQUENCY=500000
CONFIG_USB_VENDOR_ID=0x1d50
CONFIG_USB_DEVICE_ID=0x614e
CONFIG_USB_SERIAL_NUMBER_CHIPID=y
CONFIG_USB_SERIAL_NUMBER="12345"

#
# USB ids
#
# end of USB ids

# CONFIG_CUSTOM_STEP_DELAY is not set
CONFIG_INITIAL_PINS="!PC13"
CONFIG_HAVE_GPIO=y
CONFIG_HAVE_GPIO_ADC=y
CONFIG_HAVE_GPIO_SPI=y
CONFIG_HAVE_GPIO_I2C=y
CONFIG_HAVE_GPIO_HARD_PWM=y
CONFIG_HAVE_GPIO_BITBANGING=y
CONFIG_HAVE_STRICT_TIMING=y
CONFIG_HAVE_CHIPID=y
CONFIG_INLINE_STEPPER_HACK=y

```


### Step 4: Copy klipper.bin  to sd card and rename to FIRMWARE.BIN => flash firmware board SKR mini E3 V1.2


```wrap

pi@octopi:~/klipper $ pwd
/home/pi/klipper
pi@octopi:~/klipper $ ls out/
autoconf.h     board-link              compile_time_request.o    klipper.dict  src
board          compile_time_request.c  compile_time_request.txt  klipper.elf
board-generic  compile_time_request.d  klipper.bin               lib
pi@octopi:~/klipper $


```

### Step 5:

![image](https://user-images.githubusercontent.com/38026441/134792926-88b30fc9-9c0f-48b3-9f2f-5a8ef38dc552.png)


### Step 6:

![image](https://user-images.githubusercontent.com/38026441/134792966-7c1c2778-8169-4b5c-b58e-e922c04b0a12.png)


![image](https://user-images.githubusercontent.com/38026441/134792978-6795467a-0ef6-4870-8a6f-0f45d9111a6b.png)

### Step 7:

![image](https://user-images.githubusercontent.com/38026441/134793017-51418b7c-461e-4054-b9c1-c4861b09f4c2.png)


https://www.youtube.com/watch?v=T5TGLleu3MA

https://docs.vorondesign.com/build/software/miniE3_v12_klipper.html

https://www.reddit.com/r/ender3/comments/dtl8re/skr_mini_e3_12_klipper_configguide_including/

https://github.com/Klipper3d/klipper/blob/master/config/generic-bigtreetech-skr-mini-e3-v1.2.cfg


