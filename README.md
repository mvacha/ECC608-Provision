# ECC608-Provisioning

This writes certificates which are generated by python scripts in "scripts" folder to ATECC608 secure chip from ESP32 and read back them and verify the results.
after all process done, ATECC608 will be ready to use the certificates.

# Requirements

  Platformio with VS Code environment.
  install "Espressif 32" platform definition on Platformio

# Environment reference
  
  Espressif ESP32-DevkitC
  this project initialize both of I2C 0,1 port, and the device on I2C port 0 is absent.
  pin assined as below:


      I2C 0 SDA GPIO_NUM_18
      I2C 0 SCL GPIO_NUM_19

      I2C 1 SDA GPIO_NUM_21
      I2C 1 SCL GPIO_NUM_22
          
  Microchip ATECC608(on I2C port 1)

# Usage

you need to change a serial port number which actually connected to ESP32 in platformio.ini.

# Run this project

At first, you need to create self-signed CA chain by using python scripts step-by-step in "scripts" folder for test purpose.  
the scripts will generate "cert_chain.c" and "provision.h" which is mandatory to compile main C source code.  
You need to place 2 of them in "src" folder and,then execute "Upload" on Platformio. 

# Result

If you run this project with success, you can get the results on serial console as follows:

```
SPIWP:0xee
clk_drv:0x00,q_drv:0x00,d_drv:0x00,cs0_drv:0x00,hd_drv:0x00,wp_drv:0x00
mode:DIO, clock div:2
load:0x3fff0018,len:4
load:0x3fff001c,len:5804
load:0x40078000,len:7924
load:0x40080000,len:5916
entry 0x40080314
I (29) boot: ESP-IDF 3.30103.190221 2nd stage bootloader
I (29) boot: compile time 05:36:32
I (29) boot: Enabling RNG early entropy source...
I (34) boot: SPI Speed      : 40MHz
I (38) boot: SPI Mode       : DIO
I (42) boot: SPI Flash Size : 4MB
I (46) boot: Partition Table:
I (50) boot: ## Label            Usage          Type ST Offset   Length
I (57) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (65) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (72) boot:  2 factory          factory app      00 00 00010000 00100000
I (80) boot: End of partition table
I (84) esp_image: segment 0: paddr=0x00010020 vaddr=0x3f400020 size=0x08578 ( 34168) map
I (105) esp_image: segment 1: paddr=0x000185a0 vaddr=0x3ffc0000 size=0x02048 (  8264) load
I (108) esp_image: segment 2: paddr=0x0001a5f0 vaddr=0x40080000 size=0x00400 (  1024) load
I (113) esp_image: segment 3: paddr=0x0001a9f8 vaddr=0x40080400 size=0x05618 ( 22040) load
I (130) esp_image: segment 4: paddr=0x00020018 vaddr=0x400d0018 size=0x16ca4 ( 93348) map
I (163) esp_image: segment 5: paddr=0x00036cc4 vaddr=0x40085a18 size=0x03664 ( 13924) load
I (174) boot: Loaded app from partition at offset 0x10000
I (174) boot: Disabling RNG early entropy source...
I (175) cpu_start: Pro cpu up.
I (178) cpu_start: Starting app cpu, entry point is 0x400816dc
I (0) cpu_start: App cpu up.
I (189) heap_init: Initializing. RAM available for dynamic allocation:
I (196) heap_init: At 3FFAFF10 len 000000F0 (0 KiB): DRAM
I (202) heap_init: At 3FFC3790 len 0001C870 (114 KiB): DRAM
I (208) heap_init: At 3FFE0440 len 00003BC0 (14 KiB): D/IRAM
I (214) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (221) heap_init: At 4008907C len 00016F84 (91 KiB): IRAM
I (227) cpu_start: Pro cpu start user code
I (245) cpu_start: Starting scheduler on PRO CPU.
I (0) cpu_start: Starting scheduler on APP CPU.
I (806) ECC608: Serial Number:
0123xxxxxxxxxxxxee
I (806) ECC608: Revision Number:
I (806) ECC608: 00
I (806) ECC608: 00
I (806) ECC608: 60
I (806) ECC608: 02
I (806) ECC608: Config Zone data:
01 23 63 7b 00 00 60 02
20 70 8f 6d ee 01 35 00
c0 00 00 01 8f 20 c4 44
87 20 87 20 8f 0f c4 36
9f 0f 82 20 0f 0f c4 44
0f 0f 0f 0f 0f 0f 0f 0f
0f 0f 0f 0f ff ff ff ff
00 00 00 00 ff ff ff ff
00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00
ff ff 00 00 00 00 00 00
33 00 1c 00 13 00 13 00
7c 00 1c 00 3c 00 33 00
3c 00 3c 00 3c 00 30 00
3c 00 3c 00 3c 00 30 00
Writing Root Public Key
Writing Signer Certificate
Writing Device Certificate
Reading Signer Certificate
Comparing Signer Certificate
Reading Device Certificate
Comparing Device Certificate

Device Provisioning Successful!
```

# License

This software is released under the MIT License, see LICENSE.
