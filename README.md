ArduinoLog - C++ Log library for Arduino devices
====================
[![Build Status](https://travis-ci.org/georg-koch/Arduino-Log.svg?branch=master)](https://travis-ci.org/georg-koch/Arduino-Log)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](http://doge.mit-license.org)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fgeorg-koch%2FArduino-Log.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fgeorg-koch%2FArduino-Log?ref=badge_shield)

*An minimalistic Logging framework  for Arduino-compatible embedded systems.*

ArduinoLog is a minimalistic framework to help the programmer output log statements to an output of choice, fashioned after extensive logging libraries such as log4cpp ,log4j and log4net. In case of problems with an application, it is helpful to enable logging so that the problem can be located. ArduinoLog is designed so that log statements can remain in the code with minimal performance cost. In order to facilitate this the loglevel can be adjusted, and (if your code is completely tested) all logging code can be compiled out. 

## Features

* Different log levels (Error, Info, Warn, Debug, Verbose )
* Supports multiple variables
* Supports formatted strings 
* Supports formatted strings from flash memory
* Fixed memory allocation (zero malloc)
* MIT License

## Tested for 

* All Arduino boards (Uno, Due, Mini, Micro, Yun...)
* ESP8266

## Downloading

This package has been published to the Arduino & PlatformIO package managers, but you can also download it from GitHub. 

- By directly loading fetching the Archive from GitHub: 
 1. Go to [https://github.com/georg-koch/Arduino-Log](https://github.com/georg-koch/Arduino-Log)
 2. Click the DOWNLOAD ZIP button in the panel on the
 3. Rename the uncompressed folder **Arduino-Log-master** to **Arduino-Log**.
 4. You may need to create the libraries subfolder if its your first library.  
 5. Place the **Arduino-Log** library folder in your **<arduinosketchfolder>/libraries/** folder. 
 5. Restart the IDE.

## Quick start

```c++
    Serial.begin(9600);
    
    // Initialize with log level and log output. 
    Log.init    (LOG_LEVEL_VERBOSE, &Serial);
    
    // Start logging text and formatted values
    Log.error   (  "Log as Error   with binary values             : %b, %B"CR  , 23  , 345808);
    Log.warning (F("Log as Warning with integer values from Flash : %d, %d"CR) , 34  , 799870);
```
or, to use serial printer
```
    // Initialize with log level and baud rate. 
    Log.init    (LOG_LEVEL_VERBOSE, 9600);

    // Start logging text and formatted values
    Log.error   (  "Log as Error   with binary values             : %b, %B"CR  , 23  , 345808);
    Log.warning (F("Log as Warning with integer values from Flash : %d, %d"CR) , 34  , 799870);
```

[See examples/Log/Log.ino](examples/Log/Log.ino)

## Usage

### Initialisation

The log library needs to be initialized with the log level of messages to show and the log output. The latter will often be the Serial interface.
Optionally, you can indicate whether to show the log type (error, debug, etc) for each line.

```
init(int level, Print* logOutput, bool showLevel)
init(int level, Print* logOutput)
init(int level, long baud)
```

The loglevels available are

```
* 0 - LOG_LEVEL_SILENT     no output 
* 1 - LOG_LEVEL_FATAL      fatal errors 
* 2 - LOG_LEVEL_ERROR      all errors  
* 3 - LOG_LEVEL_WARNING    errors, and warnings 
* 4 - LOG_LEVEL_DEBUG      errors, warnings and debug 
* 5 - LOG_LEVEL_TRACE      errors, warnings, debug & traces 
* 6 - LOG_LEVEL_VERBOSE    all 
```

example

```
    Log.begin(LOG_LEVEL_ERROR, &Serial, true);
```

### Log events

The library allows you to log on different levels by the following functions

```c++
void fatal   (const char *format, va_list logVariables); 
void error   (const char *format, va_list logVariables);
void warning (const char *format, va_list logVariables);
void debug   (const char *format, va_list logVariables);
void trace   (const char *format, va_list logVariables);
void verbose (const char *format, va_list logVariables);
```

where the format string can be used to format the log variables

```
* %s	display as string (char*)
* %c	display as single character
* %d	display as integer value
* %l	display as long value
* %x	display as hexadecimal value
* %X	display as hexadecimal value prefixed by `0x`
* %b	display as  binary number
* %B	display as  binary number, prefixed by `0b'
* %t	display as boolean value "t" or "f"
* %T	display as boolean value "true" or "false"
* %D,%F display as double value
```

The format string may come from flash memory.

examples

```c++
    Log.fatal   (F("Log as Fatal   with string value from Flash   : %s"     CR) , "value"     );
    Log.error   (  "Log as Error   with binary values             : %b, %B" CR  , 23  , 345808);
    Log.warning (F("Log as Warning with integer values from Flash : %d, %d" CR) , 34  , 799870);
    Log.debug   (  "Log as Debug   with hexadecimal values        : %x, %X" CR  , 21  , 348972);
    Log.verbose (F("Log as Verbose with bool value from Flash     : %t, %T" CR) , true, false );
```

### Disable library

If you want to fully remove all logging code, add build flag `DISABLE_LOGGING=1`.This may significantly reduce your project size.

## Credit

Based on library by 
* [thijse](https://github.com/thijse/)

Bugfixes & features by
* [rahuldeo2047](https://github.com/rahuldeo2047)
* [NOX73](https://github.com/NOX73)
* [dhylands](https://github.com/dhylands)


## On using and modifying libraries

- [http://www.arduino.cc/en/Main/Libraries](http://www.arduino.cc/en/Main/Libraries)
- [http://www.arduino.cc/en/Reference/Libraries](http://www.arduino.cc/en/Reference/Libraries) 

## Copyright

ArduinoLog is provided Copyright © 2018 under MIT License.


## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fgeorg-koch%2FArduino-Log.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fgeorg-koch%2FArduino-Log?ref=badge_large)