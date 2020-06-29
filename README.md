# LITTLEFS

## LittleFS library for arduino-esp32

- A LittleFS wrapper for Arduino ESP32 of [Mbed LittleFS](https://github.com/ARMmbed/littlefs)
- Based on [ESP-IDF port of joltwallet/esp_littlefs](https://github.com/joltwallet/esp_littlefs) , thank you Brian!
- See also the [LillteFS library for ESP8266 core](https://github.com/esp8266/Arduino/tree/master/libraries/LittleFS) 
- Functionality is similar to SPIFFS
- Either LITTLEFS or SPIFFS but not both simultaneously can be used in same Arduino project
- [Related PR in esp32 core development](https://github.com/espressif/arduino-esp32/pull/4096) 
- See also the [LillteFS library for ESP8266 core](https://github.com/esp8266/Arduino/tree/master/libraries/LittleFS) 

##### Warning: It depends on ESP-IDF, esp32 core, esp_littlefs and Mbed LittleFS versions

- Tested with [esp32-core #git b92c58d](https://github.com/espressif/arduino-esp32/commit/b92c58d74b151c7a3b56db4e78f2d3c90c16446f) and on core [release 1.0.4](https://github.com/espressif/arduino-esp32/releases/tag/1.0.4)

### Installation

- Copy <b>LITTLEFS</b> to other Arduino IDE libraries
</br>(see File > Preferences > Sketchbook location). 

### Usage

- use LITTLEFS same way as SPIFFS
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
### Differences with SPIFFS (and in this implementation)

- LittleFS has folders, you my need to tweak your code to iterate files in folders
- Root: /someting  = something, so attention to /
- Lower level littlefs library cannot mount on NULL as partition_label name, while SPIFFS can
- Lower level littlefs library does not need maxOpenFiles parameter
- Speed (LITTLEFS_Test.ino) 1048576 bytes written in 16238 ms / 1048576 bytes read in 918 ms
- Speed (SPIFFS_Test.ino)   1048576 bytes written in 65971 ms / 1048576 bytes read in 680 ms


### Arduino ESP32 LittleFS filesystem upload tool 

- Download the jar file from [here](https://github.com/lorol/arduino-esp32littlefs-plugin/raw/master/src/bin/esp32littlefs.jar)
- In your Arduino sketchbook directory, create tools directory if it doesn't exist yet.
- Copy the tool into tools directory ```<home_dir>/Arduino/tools/ESP32LittleFS/tool/esp32littlefs.jar```
- Requires [mklittlefs executable](https://github.com/earlephilhower/mklittlefs) - download the zipped binary from [here](https://github.com/earlephilhower/mklittlefs/releases) or <b>esp-quick-toolchain</b> [here](https://github.com/earlephilhower/esp-quick-toolchain/releases) 
- Copy the binary to ```packages\esp32\hardware\esp32\<x.x.x>\tools\mklittlefs\``` folder
- Restart Arduino IDE. 

## Credits and license

- This work is based on [Mbed LittleFS](https://github.com/ARMmbed/littlefs) , [ESP-IDF port of joltwallet/esp_littlefs](https://github.com/joltwallet/esp_littlefs) , [Espressif Arduino core for the ESP32, the ESP-IDF - SPIFFS Library](https://github.com/espressif/arduino-esp32/tree/master/libraries/SPIFFS)
- Licensed under GPL v2 ([text](LICENSE))
