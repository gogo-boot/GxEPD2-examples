# 🔧 Display Configuration Reference

## Common Display Types & Configuration

### Finding Your Display Model

**Check the back of your display** for a model number like:
- `GDEH0154D67` (1.54")
- `GDEH0213B73` (2.13") 
- `GDEH029A1` (2.9")
- `GDEH042T2` (4.2")

### Configuration Steps

1. **Edit the shared display configuration file**:
   ```
   include/GxEPD2_display_selection_new_style.h
   ```

2. **Find and uncomment your display**:
   ```cpp
   // Search for your model number and uncomment:
   #define GxEPD2_DRIVER_CLASS GxEPD2_154_D67  // Your display here
   ```

3. **Save the file** - This configuration will apply to ALL examples

**✅ Advantage:** Configure once, use with all examples!

## Display Model Reference

### 1.54" Displays (200x200)
```cpp
#define GxEPD2_DRIVER_CLASS GxEPD2_154_D67    // GDEH0154D67 - Common
#define GxEPD2_DRIVER_CLASS GxEPD2_154_M09    // GDEH0154M09 - Variant
#define GxEPD2_DRIVER_CLASS GxEPD2_154_M10    // GDEH0154M10 - Variant
```

### 2.13" Displays (250x122)
```cpp
#define GxEPD2_DRIVER_CLASS GxEPD2_213_B72    // GDEH0213B72 - Common
#define GxEPD2_DRIVER_CLASS GxEPD2_213_B73    // GDEH0213B73 - Newer
#define GxEPD2_DRIVER_CLASS GxEPD2_213_flex   // Flexible variants
```

### 2.9" Displays (296x128)
```cpp
#define GxEPD2_DRIVER_CLASS GxEPD2_290_T5D    // GDEH029T5D - Common
#define GxEPD2_DRIVER_CLASS GxEPD2_290_T94    // GDEH029T94 - Variant
#define GxEPD2_DRIVER_CLASS GxEPD2_290_M06    // GDEH029M06 - Variant
```

### 4.2" Displays (400x300)
```cpp
#define GxEPD2_DRIVER_CLASS GxEPD2_420_T94    // GDEH042T94 - Common
#define GxEPD2_DRIVER_CLASS GxEPD2_420_M01    // GDEH042M01 - Variant
```

### 7.5" Displays (800x480)
```cpp
#define GxEPD2_DRIVER_CLASS GxEPD2_750_T7     // GDEH075T7 - Common
#define GxEPD2_DRIVER_CLASS GxEPD2_750_Z08    // GDEH075Z08 - Variant
```

## Color Display Types

### Select Display Class

Along with the driver, select the appropriate display class:

```cpp
// Black & White displays
#define GxEPD2_DISPLAY_CLASS GxEPD2_BW

// 3-Color displays (Black, White, Red/Yellow)
#define GxEPD2_DISPLAY_CLASS GxEPD2_3C

// 4-Color displays  
#define GxEPD2_DISPLAY_CLASS GxEPD2_4C

// 7-Color displays (ACeP)
#define GxEPD2_DISPLAY_CLASS GxEPD2_7C
```

## Pin Configuration

### Default ESP32 Pins
```cpp
// These are the default pins used in examples
#define EPD_CS    27  // Chip Select
#define EPD_DC    14  // Data/Command
#define EPD_RST   12  // Reset
#define EPD_BUSY  13  // Busy
// MOSI = 23, SCK = 18 (fixed SPI pins)
```

### Custom Pin Configuration

If you need different pins, edit the display constructor:

```cpp
// Example: Custom ESP32 pins
GxEPD2_BW<GxEPD2_154_D67, GxEPD2_154_D67::HEIGHT> display(
    GxEPD2_154_D67(
        /*CS=*/ 5,   // Your CS pin
        /*DC=*/ 17,  // Your DC pin  
        /*RST=*/ 16, // Your RST pin
        /*BUSY=*/ 4  // Your BUSY pin
    )
);
```

## Board-Specific Notes

### ESP8266 (D1 Mini)
```cpp
// Typical D1 Mini pins
#define EPD_CS    15  // D8
#define EPD_DC    0   // D3
#define EPD_RST   2   // D4
#define EPD_BUSY  4   // D2
```

### Arduino Uno/Nano
```cpp
// Standard Arduino pins
#define EPD_CS    7   
#define EPD_DC    6   
#define EPD_RST   5   
#define EPD_BUSY  4   
```

## Troubleshooting Display Issues

### Display Not Responding
1. **Check power**: Must be 3.3V, not 5V
2. **Check wiring**: Especially CS, DC, RST, BUSY pins
3. **Check model**: Make sure display selection matches your hardware
4. **Try different example**: Start with hello_world

### Wrong Display Size/Orientation
1. **Verify model number** on the back of your display
2. **Check display class** (BW, 3C, 4C, 7C)
3. **Try different drivers** of the same size if unsure

### Poor Display Quality
1. **Check power supply**: Use adequate current capacity (>500mA)
2. **Add capacitors**: 100µF electrolytic + 10µF ceramic
3. **Check connections**: Ensure solid connections
4. **Temperature**: Some displays perform poorly outside 0-40°C

## Need Help?

If your display isn't listed or isn't working:

1. **Check the GxEPD2 library documentation**: https://github.com/ZinggJM/GxEPD2
2. **Look at the full display selection file** for more options
3. **Search for your specific model** in Arduino forums
4. **Try similar size displays** as a starting point
