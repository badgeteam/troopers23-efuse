# ESP32 component: eFuse functions

An ESP-IDF component for managing the eFuses of the ESP32 on the TROOPERS23 badge.

Defines two functions:

## void efuse_print_state()

Prints an incomplete report on the state of the eFuses to the console.

## void efuse_protect()

1. Forces 3.3v operation for the SPI flash and PSRAM on the ESP32 module. The TROOPERS23 badge uses an "ESP32-WROVER-E" module. If your device uses a different module type (like the original non -E version of the "ESP32-WROVER") then you either want to modify this function or stay away from it all together as those modules use 1.8v flash and PSRAM.
2. Write protects all dangerous eFuses

## eFuse summary after running the efuse protect function

```
espefuse.py v3.3-dev
EFUSE_NAME (Block) Description  = [Meaningful Value] [Readable/Writeable] (Hex Value)
----------------------------------------------------------------------------------------
Calibration fuses:
BLK3_PART_RESERVE (BLOCK0):                        BLOCK3 partially served for ADC calibration data   = False R/- (0b0)
ADC_VREF (BLOCK0):                                 Voltage reference calibration                      = 1107 R/- (0b00001)

Config fuses:
XPD_SDIO_FORCE (BLOCK0):                           Ignore MTDI pin (GPIO12) for VDD_SDIO on reset     = True R/- (0b1)
XPD_SDIO_REG (BLOCK0):                             If XPD_SDIO_FORCE, enable VDD_SDIO reg on reset    = True R/- (0b1)
XPD_SDIO_TIEH (BLOCK0):                            If XPD_SDIO_FORCE & XPD_SDIO_REG                   = 3.3V R/- (0b1)
CLK8M_FREQ (BLOCK0):                               8MHz clock freq override                           = 50 R/W (0x32)
SPI_PAD_CONFIG_CLK (BLOCK0):                       Override SD_CLK pad (GPIO6/SPICLK)                 = 0 R/- (0b00000)
SPI_PAD_CONFIG_Q (BLOCK0):                         Override SD_DATA_0 pad (GPIO7/SPIQ)                = 0 R/- (0b00000)
SPI_PAD_CONFIG_D (BLOCK0):                         Override SD_DATA_1 pad (GPIO8/SPID)                = 0 R/- (0b00000)
SPI_PAD_CONFIG_HD (BLOCK0):                        Override SD_DATA_2 pad (GPIO9/SPIHD)               = 0 R/- (0b00000)
SPI_PAD_CONFIG_CS0 (BLOCK0):                       Override SD_CMD pad (GPIO11/SPICS0)                = 0 R/- (0b00000)
DISABLE_SDIO_HOST (BLOCK0):                        Disable SDIO host                                  = False R/W (0b0)

Efuse fuses:
WR_DIS (BLOCK0):                                   Efuse write disable mask                           = 46701 R/W (0xb66d)
RD_DIS (BLOCK0):                                   Efuse read disable mask                            = 0 R/- (0x0)
CODING_SCHEME (BLOCK0):                            Efuse variable block length scheme                
   = NONE (BLK1-3 len=256 bits) R/- (0b00)
KEY_STATUS (BLOCK0):                               Usage of efuse block 3 (reserved)                  = False R/- (0b0)

Identity fuses:
MAC (BLOCK0):                                      Factory MAC Address                               
   = b8:f0:09:91:f6:a8 (CRC 0x4e OK) R/- 
MAC_CRC (BLOCK0):                                  CRC8 for factory MAC address                       = 78 R/- (0x4e)
CHIP_VER_REV1 (BLOCK0):                            Silicon Revision 1                                 = True R/- (0b1)
CHIP_VER_REV2 (BLOCK0):                            Silicon Revision 2                                 = True R/- (0b1)
CHIP_VERSION (BLOCK0):                             Reserved for future chip versions                  = 2 R/- (0b10)
CHIP_PACKAGE (BLOCK0):                             Chip package identifier                            = 1 R/- (0b001)
MAC_VERSION (BLOCK3):                              Version of the MAC field                           = 0 R/- (0x00)

Security fuses:
FLASH_CRYPT_CNT (BLOCK0):                          Flash encryption mode counter                      = 0 R/- (0b0000000)
UART_DOWNLOAD_DIS (BLOCK0):                        Disable UART download mode (ESP32 rev3 only)       = False R/- (0b0)
FLASH_CRYPT_CONFIG (BLOCK0):                       Flash encryption config (key tweak bits)           = 0 R/- (0x0)
CONSOLE_DEBUG_DISABLE (BLOCK0):                    Disable ROM BASIC interpreter fallback             = True R/- (0b1)
ABS_DONE_0 (BLOCK0):                               Secure boot V1 is enabled for bootloader image     = False R/- (0b0)
ABS_DONE_1 (BLOCK0):                               Secure boot V2 is enabled for bootloader image     = False R/- (0b0)
JTAG_DISABLE (BLOCK0):                             Disable JTAG                                       = False R/W (0b0)
DISABLE_DL_ENCRYPT (BLOCK0):                       Disable flash encryption in UART bootloader        = False R/- (0b0)
DISABLE_DL_DECRYPT (BLOCK0):                       Disable flash decryption in UART bootloader        = False R/- (0b0)
DISABLE_DL_CACHE (BLOCK0):                         Disable flash cache in UART bootloader             = False R/- (0b0)
BLOCK1 (BLOCK1):                                   Flash encryption key                              
   = 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 R/W 
BLOCK2 (BLOCK2):                                   Secure boot key                                   
   = 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 R/W 
BLOCK3 (BLOCK3):                                   Variable Block 3                                  
   = 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 R/- 

Flash voltage (VDD_SDIO) set to 3.3V by efuse.
```

## But what if I want to play with efuses?

You're free to burn whatever you want to blocks 1 and 2, they've not been write protected but the read protection is permanently disabled by the protect function so they can always be read.

## License

This ESP32 module has been written by Renze Nicolai and may be used under the terms of the MIT license.
