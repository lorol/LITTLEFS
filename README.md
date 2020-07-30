# LITTLEFS

## LittleFS library for arduino-esp32

- A LittleFS wrapper for Arduino ESP32 of [Mbed LittleFS](https://github.com/ARMmbed/littlefs)
- Based on [ESP-IDF port of joltwallet/esp_littlefs](https://github.com/joltwallet/esp_littlefs) , thank you Brian!
- See also the [LillteFS library for ESP8266 core](https://github.com/esp8266/Arduino/tree/master/libraries/LittleFS) 
- Functionality is similar to SPIFFS
- [Related PR at esp32 core development](https://github.com/espressif/arduino-esp32/pull/4096) 
- [Related PR at esp-idf development](https://github.com/espressif/esp-idf/pull/5469)
```diff
! Warning: This wrapper depends on ESP-IDF, esp32 core, esp_littlefs and Mbed LittleFS versions
```
- Tested with esp32 cores built on IDFv3.2, IDFv3.3 and esp32s2 on IDFv4.2 
- For esp32 core release 1.0.4 w/ IDFv3.2 you need to uncomment this line in **esp_littlefs.c**:  ```//#define CONFIG_LITTLEFS_FOR_IDF_3_2```
- See LITTLEFS_time example with file timestamps that works with esp32 core on IDF v3.3

### Installation

- Copy **LITTLEFS** to Arduino IDE **/libraries** folder (File > Preferences > Sketchbook location). 

### Usage

- Use LITTLEFS same way as SPIFFS
- A quick startup based on your existing code you can re-define SPIFFS like this 
``` 
#define USE_LittleFS

#include <FS.h>
#ifdef USE_LittleFS
  #define SPIFFS LITTLEFS
  #include <LITTLEFS.h> 
#else
  #include <SPIFFS.h>
#endif 
 ```
### Differences with SPIFFS 

- LittleFS has folders, you need need to iterate files in folders
- At root a "/folder" = "folder"
- Requires a label for mount point, NULL will not work
- maxOpenFiles parameter is unused, kept for compatibility
- LITTLEFS.mkdir(path) and  LITTLEFS.rmdir(path) work as expected for folders
- Speed comparison based on **LittleFS_test.ino** sketch (for a file 1048576 bytes):

|Filesystem|Read time [ms]|Write time [ms]|
|----|----|----|
|FAT|276|14493|
|LITTLEFS|446*|16387|
|SPIFFS|767|65622|

*The read speed improved by changing ```#define CONFIG_LITTLEFS_CACHE_SIZE``` from 128 to 512


### Arduino ESP32 LittleFS filesystem upload tool 

- Use (replace if exists) [arduino-esp32fs-plugin](https://github.com/me-no-dev/arduino-esp32fs-plugin/pull/23 ) with [this variant](https://github.com/lorol/arduino-esp32fs-plugin), which supports SPIFFS, LittleFS and FatFS
- Requires [mklittlefs executable](https://github.com/earlephilhower/mklittlefs) which is available [in releases section here](https://github.com/lorol/arduino-esp32fs-plugin ) or download the zipped binary [here](https://github.com/earlephilhower/mklittlefs/releases) or from **esp-quick-toolchain** releases [here](https://github.com/earlephilhower/esp-quick-toolchain/releases) 
- Copy it to **/tools** folder of esp32 platform where **espota** and **esptool** (.py or.exe) tools are located
- Restart Arduino IDE. 

### PlatformIO
 (notes from [BlueAndi](https://github.com/BlueAndi) )
- Add to _platformio.ini_:
 `extra_scripts = replace_fs.py`
 
- Add _replace_fs.py_ to project root directory (where platformio.ini is located):
 
 ```python
 Import("env")
 print("Replace MKSPIFFSTOOL with mklittlefs.exe")
 env.Replace (MKSPIFFSTOOL = "mklittlefs.exe")
 ```
 
- Add _mklittlefs.exe_ to project root directory as well.


## Credits and license

- This work is based on [Mbed LittleFS](https://github.com/ARMmbed/littlefs) , [ESP-IDF port of joltwallet/esp_littlefs](https://github.com/joltwallet/esp_littlefs) , [Espressif Arduino core for the ESP32, the ESP-IDF - SPIFFS Library](https://github.com/espressif/arduino-esp32/tree/master/libraries/SPIFFS)
- Licensed under GPL v2 ([text](LICENSE))
