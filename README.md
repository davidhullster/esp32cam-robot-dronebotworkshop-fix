# ESP32CAM Robot Car - Updated for Modern Arduino IDE

This project is an updated version of the ESP32CAM Robot Car tutorial from [DroneBot Workshop](https://dronebotworkshop.com/esp32cam-robot-car/) (2021).

## Original Tutorial
The original tutorial by DroneBot Workshop provided a great foundation for building an ESP32CAM-based robot car with web-based control interface. However, the code used deprecated libraries that no longer compile with recent Arduino IDE versions.

## Updates Made

### 1. Removed Deprecated `dl_lib_matrix3d.h` Library
- **Problem**: The original code used `dl_lib_matrix3d.h` which is no longer supported in recent ESP32 Arduino core versions
- **Solution**: Replaced with standard ESP32 camera functions
- **Changes**:
  - Removed `#include "dl_lib_matrix3d.h"`
  - Simplified `capture_handler()` function to use only supported ESP32 camera functions
  - Removed deprecated matrix allocation and RGB888 conversion code

### 2. Fixed LEDC Function Compatibility
- **Problem**: Arduino LEDC functions (`ledcAttachPin`, `ledcSetup`, `ledcWrite`) were not available or had compatibility issues
- **Solution**: Replaced with standard ESP-IDF LEDC functions
- **Changes**:
  - Added `#include "driver/ledc.h"`
  - Replaced Arduino LEDC functions with ESP-IDF equivalents:
    - `ledcAttachPin()` → `ledc_channel_config()`
    - `ledcSetup()` → `ledc_timer_config()`
    - `ledcWrite()` → `ledc_set_duty()` + `ledc_update_duty()`
  - Used standard C structure initialization to avoid field order compatibility issues

### 3. Improved Code Structure
- **Motor PWM**: Uses `LEDC_CHANNEL_0` with `LEDC_TIMER_0`
- **LED Flash**: Uses `LEDC_CHANNEL_1` with `LEDC_TIMER_1`
- **Compatibility**: Works with any ESP-IDF version regardless of structure field order

## Files Updated
- `esp32cam.ino` - Main Arduino sketch
- `app_httpd.cpp` - HTTP server and robot control functions

## Hardware Requirements
- ESP32CAM module
- TB6612FNG H-Bridge motor controller
- DC motors and wheels
- Power supply (5V for ESP32CAM, separate supply for motors)
- FTDI adapter for programming

## Features
- Web-based control interface
- Real-time camera streaming
- Motor speed control
- LED flash control
- Mobile-friendly interface

## Compilation
This updated code should compile successfully with:
- Arduino IDE 2.x
- ESP32 Arduino Core 2.x or 3.x
- Recent ESP-IDF versions

## Credits
Original tutorial and code by [DroneBot Workshop](https://dronebotworkshop.com/esp32cam-robot-car/)
Updates made to ensure compatibility with modern development environments.
