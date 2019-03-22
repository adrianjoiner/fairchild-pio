## VS Code plugins
- PlatformIO
- C/C++ Intellisense

__Care to disable or uninstall the Arduino plugin__

## Libraries
Care to __clone__ these (and any new libraries) into the pio libs folder and use as git submodules as necessary. 
eg 
```
# inside the lib folder
git submodule add https://github.com/adafruit/Adafruit_BMP280_Library.git 
git submodule add https://github.com/KenjutsuGH/Adafruit-PCD8544-Nokia-5110-LCD-library.git
```

### Libraries currently used
[MPU9250](https://github.com/bolderflight/MPU9250)
[Adafruit_BMP280_Library](https://github.com/adafruit/Adafruit_BMP280_Library)
[Ported Adafruit PCD8544 - Nokia 5110](https://github.com/KenjutsuGH/Adafruit-PCD8544-Nokia-5110-LCD-library)
[Roger clarks Adafruit_STM32](https://github.com/rogerclarkmelbourne/Arduino_STM32.git)

### Notes if using the VS Code and the Arduino IDE - .cpp, .c and .ino files
__.ino files__ : during compile time, the compiler joins all the .ino files together, in alphabetical order (except the 'main' .ino) and compiles as one big file. 
__.cpp / .h files__ : each file is compiled independently, this is standard c++ behaviour

Big multifile projects - use .cpp, small projects use .ino

Something to be aware of when deconstructing other peoples code made of multiple .ino files as they appear to be missing a heap of imports and variable declarations etc.

Don't mix and match

__Note__ #include "Adafruit_GFX.h" needed to be addded to the Adafruit_PCD8544.h file and the library addded using the library manager, which installed the library as a global library and not in the project library

## Setting build output file / arduino.json settings
[arduino.json settings](https://arduino.stackexchange.com/questions/45347/warning-when-verifying-sketch-with-vs-code)


# Design decisions
- VS Code / Arduino plugin + Arduino IDE
- Use __.ino__ files for main program and its functions. __.cpp__ if you need to create a library


# Connecting an STM32 to RC reciever using PPM
[Info](https://www.youtube.com/watch?v=JFSFbSg0l2M&feature=youtu.be)
 The video and examples use this library that needs to be places inside ~/Documents/Arduino/hardware/Arduino_STM32

- Utilises STM32 input capture mode to calculate width of recieved pulses

### Connections
RX: GND > GND
RX: VCC > 3.3v
RX: PPM output, simgle wire >> A0 on STM32

https://github.com/rogerclarkmelbourne/Arduino_STM32/archive/master.zip

# STM32
[Support site](http://www.stm32duino.com)
https://github.com/rogerclarkmelbourne/Arduino_STM32/archive/master.zip

## Connect STM32 to Nokia 5110
Using forked [Adafruit-PCD8544-Nokia-5110-LCD-library](https://github.com/KenjutsuGH/Adafruit-PCD8544-Nokia-5110-LCD-library.git) which needs to be cloned into 
[also here ](https://randomnerdtutorials.com/complete-guide-for-nokia-5110-lcd-with-arduino/) for example code
[Nokia5110 lcd](https://lastminuteengineers.com/nokia-5110-lcd-arduino-tutorial/)

The screen is graphic, ie not char based, but can contain 6 rows of 12 chars


## Travis CI
[Build PR's and pushes to master only](https://stackoverflow.com/questions/31882306/how-to-configure-travis-ci-to-build-pull-requests-merges-to-master-w-o-redunda)