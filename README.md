# GxEPD2 Examples - PlatformIO Project

A comprehensive PlatformIO project containing all GxEPD2 library examples, converted from Arduino IDE format and optimized for easy development and testing with e-paper displays.

## 📚 Documentation

- **🚀 [QUICK_START.md](QUICK_START.md)** - Get running in 30 seconds
- **🎯 [EXAMPLES_GUIDE.md](EXAMPLES_GUIDE.md)** - Which example should you use?
- **🔧 [DISPLAY_CONFIG.md](DISPLAY_CONFIG.md)** - Configure your specific display
- **🐛 [TROUBLESHOOTING.md](TROUBLESHOOTING.md)** - Fix common problems

## 🚀 Quick Start

### Prerequisites
- [PlatformIO Core](https://docs.platformio.org/en/latest/core/installation.html) or [PlatformIO IDE](https://platformio.org/install/ide)
- ESP32, ESP8266, Arduino Uno, or STM32 development board
- Compatible e-paper display (see [Supported Displays](#supported-displays))

### ⚡ Run Your First Example

**New to this project? Start with the [🚀 Quick Start Guide](QUICK_START.md)**

1. **Clone and enter the project:**
   ```bash
   cd GxEPD2-examples
   ```

2. **Configure your display (REQUIRED):**
   Edit `src/GxEPD2_HelloWorld/GxEPD2_display_selection_new_style.h`:
   ```cpp
   // Uncomment your display type
   #define GxEPD2_DRIVER_CLASS GxEPD2_154_D67  // For 1.54" displays
   ```
   **📖 Need help?** See [DISPLAY_CONFIG.md](DISPLAY_CONFIG.md)

3. **Build and upload:**
   ```bash
   pio run -e hello_world -t upload
   ```

4. **Monitor output:**
   ```bash
   pio device monitor -e hello_world
   ```

**🎯 Not sure which example to use?** Check [EXAMPLES_GUIDE.md](EXAMPLES_GUIDE.md)

## Project Structure

```
GxEPD2-examples/
├── platformio.ini          # PlatformIO configuration with all environments
├── lib/
│   └── GxEPD2/             # Local GxEPD2 library reference
│       ├── library.json    # Library metadata
│       └── src/            # Symbolic link to parent library
├── src/                    # All example source code
│   ├── GxEPD2_HelloWorld/  # Basic "Hello World" example
│   ├── GxEPD2_Example/     # Comprehensive display example
│   ├── GxEPD2_GFX_Example/ # Graphics and text examples
│   └── ...                 # All other examples
└── README.md               # This documentation
```

## 📋 Available Examples

| Environment | Description | Board | Special Dependencies |
|-------------|-------------|-------|---------------------|
| `hello_world` | **START HERE** - Basic "Hello World" display | ESP32 | None |
| `basic_example` | Comprehensive GxEPD2 features demo | ESP32 | None |
| `gfx_example` | Graphics, fonts, and text rendering | ESP32 | None |
| `multi_display` | Multiple display handling | ESP32 | None |
| `not_paged` | Non-paged display (direct drawing) | ESP32 | None |
| `paged_callback` | Memory-efficient paged rendering | ESP32 | None |
| `rotary_callback` | Rotary encoder integration | ESP32 | None |
| `sd_example` | SD card image loading/saving | ESP32 | SD Library |
| `sd_avr_example` | SD card for Arduino Uno/Nano | Arduino Uno | SD Library |
| `sd_write_bitmap` | Write bitmaps to SD card | ESP32 | SD Library |
| `serial_flash_example` | Serial flash storage | ESP32 | None |
| `serial_flash_loader` | Load images from serial flash | ESP32 | None |
| `spiffs_example` | SPIFFS filesystem integration | ESP32 | None |
| `u8g2_fonts` | U8G2 font library integration | ESP32 | U8g2 Library |
| `ws_esp32_driver` | Waveshare ESP32 e-Paper driver | ESP32 | None |
| `fast_bw_on_color` | Fast B&W rendering on color displays | ESP32 | None |
| `mixed_test` | Mixed display testing | ESP32 | None |

### 🔧 Board Variants

Each example has multiple board variants available:
- `*_esp8266` - ESP8266 (D1 Mini, NodeMCU) 
- `*_uno` - Arduino Uno/Nano/Pro Mini
- `*_esp32s3` - ESP32-S3 DevKit
- `*_stm32` - STM32 Nucleo boards

**Example:** `hello_world_esp8266`, `basic_example_uno`, `gfx_example_esp32s3`

## 🛠️ Essential Configuration

### Step 1: Select Your Display

**⚠️ CRITICAL:** You MUST configure your display type before the examples will work!

Edit the display selection file in your chosen example:
```
src/[EXAMPLE_NAME]/GxEPD2_display_selection_new_style.h
```

**Common Display Configurations:**

```cpp
// For 1.54" displays (200x200)
#define GxEPD2_DRIVER_CLASS GxEPD2_154_D67

// For 2.13" displays (250x122) 
#define GxEPD2_DRIVER_CLASS GxEPD2_213_B73

// For 2.9" displays (296x128)
#define GxEPD2_DRIVER_CLASS GxEPD2_290_T5D

// For 4.2" displays (400x300)
#define GxEPD2_DRIVER_CLASS GxEPD2_420_T94

// For 7.5" displays (800x480)
#define GxEPD2_DRIVER_CLASS GxEPD2_750_T7
```

### Step 2: Verify Wiring

Check `GxEPD2_wiring_examples.h` in your example folder for wiring diagrams.

**Standard ESP32 Wiring:**
```
Display Pin -> ESP32 Pin
VCC         -> 3.3V
GND         -> GND
DIN (MOSI)  -> GPIO23
CLK (SCK)   -> GPIO18
CS          -> GPIO27
DC          -> GPIO14
RST         -> GPIO12
BUSY        -> GPIO13
```

**Standard ESP8266 Wiring (D1 Mini):**
```
Display Pin -> D1 Mini Pin
VCC         -> 3.3V
GND         -> GND
DIN (MOSI)  -> D7 (GPIO13)
CLK (SCK)   -> D5 (GPIO14)
CS          -> D8 (GPIO15)
DC          -> D3 (GPIO0)
RST         -> D4 (GPIO2)
BUSY        -> D2 (GPIO4)
```

### Step 3: Power Requirements

**⚠️ IMPORTANT:**
- E-paper displays require **3.3V power supply**
- Current draw during refresh: **20-40mA**
- Use external 3.3V regulator for battery projects

## 🚀 Usage & Commands

### PlatformIO Commands

#### Basic Operations
```bash
# List all available environments
pio project config

# Build specific example
pio run -e hello_world

# Build and upload
pio run -e hello_world -t upload

# Clean build files
pio run -e hello_world -t clean

# Monitor serial output (after upload)
pio device monitor -e hello_world
```

#### Advanced Operations
```bash
# Build all examples
pio run

# Upload with custom port
pio run -e hello_world -t upload --upload-port /dev/ttyUSB0

# Build with verbose output
pio run -e hello_world -v

# Install additional libraries
pio pkg install --library "adafruit/Adafruit BusIO"
```

### VS Code Integration

1. **Install PlatformIO Extension**
2. **Open project folder**
3. **Use PlatformIO toolbar:**
   - Click "Build" (✓) to compile
   - Click "Upload" (→) to flash
   - Click "Monitor" (🔌) for serial output
   - Use environment selector in status bar

### Getting Started Workflow

1. **Start with Hello World:**
   ```bash
   pio run -e hello_world -t upload && pio device monitor -e hello_world
   ```

2. **Configure your display** (see [Essential Configuration](#🛠️-essential-configuration))

3. **Try other examples:**
   ```bash
   pio run -e gfx_example -t upload
   pio run -e basic_example -t upload
   ```

## 🖥️ Supported Displays

### Monochrome (Black & White)
- **1.54"** - GDEH0154D67 (200x200)
- **2.13"** - GDEH0213B73/GDEH0213B72 (250x122)
- **2.9"** - GDEH029A1/GDEH029T5D (296x128)
- **4.2"** - GDEH042T2/GDEH042Z96 (400x300)
- **7.5"** - GDEH075T7/GDEH075Z08 (800x480)

### Three-Color (Black, White, Red/Yellow)
- **1.54"** - GDEH0154Z90 (200x200)
- **2.13"** - GDEH0213Z19 (250x122) 
- **2.9"** - GDEH029Z10 (296x128)
- **4.2"** - GDEH042Z21 (400x300)

### Advanced Color Displays
- **7-Color ACeP** - GDEH073D46 (800x480)
- **4-Color** - Various models

**🔍 Find Your Display:** Check the model number on the back of your display and match it in the `GxEPD2_display_selection_new_style.h` file.

**📖 Need detailed help?** See [DISPLAY_CONFIG.md](DISPLAY_CONFIG.md) for complete configuration guide.

## 🔧 Advanced Configuration

### Custom Board Support

Add new boards by creating environments in `platformio.ini`:

```ini
[env:my_custom_esp32]
extends = env:hello_world
platform = espressif32
board = esp32-c3-devkitm-1
build_flags = 
    ${env.build_flags}
    -DBOARD_HAS_PSRAM
    -DARDUINO_USB_CDC_ON_BOOT=1
```

### Custom Display Configuration

For displays not in the predefined list:

```cpp
// In your example's display selection file
// Add custom display constructor
GxEPD2_BW<GxEPD2_custom, GxEPD2_custom::HEIGHT> display(
    GxEPD2_custom(
        /*CS=*/ 27, 
        /*DC=*/ 14, 
        /*RST=*/ 12, 
        /*BUSY=*/ 13
    )
);
```

### Build Flags & Options

Common build flags you can add to `platformio.ini`:

```ini
build_flags = 
    ${env.build_flags}
    -DENABLE_GxEPD2_GFX=1          # Enable extended GFX features
    -DSERIAL_DEBUG=1               # Enable debug output
    -DCORE_DEBUG_LEVEL=3           # ESP32 debug level
    -DBOARD_HAS_PSRAM              # Enable PSRAM support
```

## 🐛 Troubleshooting

### Common Issues & Solutions

#### ❌ "Display not working" / "Nothing appears"

**Check:**
1. **Display selection configured?** ✅ Edit `GxEPD2_display_selection_new_style.h`
2. **Power supply is 3.3V?** ✅ Measure VCC pin
3. **Wiring correct?** ✅ Check pin connections
4. **Reset timing?** ✅ Try different RST pin

**Test command:**
```bash
pio run -e hello_world -t upload && pio device monitor -e hello_world
```

#### ❌ "Compilation failed" / "Missing files"

**Check:**
1. **PlatformIO up to date?**
   ```bash
   pio upgrade
   ```
2. **Dependencies installed?**
   ```bash
   pio pkg install
   ```
3. **Clean build:**
   ```bash
   pio run -e hello_world -t clean
   pio run -e hello_world
   ```

#### ❌ "Upload failed" / "Device not found"

**Check:**
1. **Correct USB port?**
   ```bash
   pio device list
   pio run -e hello_world -t upload --upload-port /dev/ttyUSB0
   ```
2. **Board in bootloader mode?** Hold BOOT button during upload
3. **USB cable data-capable?** Try different cable

#### ❌ "Display artifacts" / "Partial updates"

**Solutions:**
- Increase power supply capacity (min. 500mA)
- Add decoupling capacitors (100µF + 10µF)
- Check for loose connections
- Reduce SPI speed in code if needed

### Debug Mode

Enable verbose debugging:

```cpp
// Add to your code
#define SERIAL_DEBUG 1
```

Build with debug:
```bash
pio run -e hello_world -v
```

### Getting Help

**📚 Check our documentation first:**
- [🚀 QUICK_START.md](QUICK_START.md) - 30-second setup guide
- [🐛 TROUBLESHOOTING.md](TROUBLESHOOTING.md) - Common problems & solutions  
- [🔧 DISPLAY_CONFIG.md](DISPLAY_CONFIG.md) - Display configuration help
- [🎯 EXAMPLES_GUIDE.md](EXAMPLES_GUIDE.md) - Example selection guide

**Still need help?**
1. **Check GxEPD2 Wiki:** https://github.com/ZinggJM/GxEPD2/wiki
2. **Arduino Forum:** https://forum.arduino.cc/c/using-arduino/displays/23
3. **PlatformIO Docs:** https://docs.platformio.org/
4. **Hardware Issues:** Check your display manufacturer's documentation

## 📚 Dependencies & Libraries

### Automatic Dependencies
These are installed automatically via `platformio.ini`:

- **Adafruit GFX Library** `^1.11.9` - Core graphics library (ALL examples)
- **SD Library** - SD card support (SD examples only)  
- **U8g2** `^2.35.19` - Advanced fonts (U8G2 examples only)

### Manual Installation
For additional functionality:

```bash
# Advanced graphics
pio pkg install --library "adafruit/Adafruit BusIO"

# JSON parsing  
pio pkg install --library "bblanchon/ArduinoJson"
```

## 🔄 Project Maintenance

### Update Dependencies
```bash
# Update all libraries
pio pkg update

# Update specific library
pio pkg update --library "adafruit/Adafruit GFX Library"
```

### Add New Examples

1. **Create example directory:**
   ```bash
   mkdir src/MyNewExample
   ```

2. **Add to platformio.ini:**
   ```ini
   [env:my_new_example]
   board = esp32dev
   build_src_filter = +<MyNewExample/>
   ```

3. **Copy template files:**
   ```bash
   cp src/GxEPD2_HelloWorld/*.h src/MyNewExample/
   ```

## 📄 License

This project follows the same license as the GxEPD2 library: **GPL-3.0**

## 🤝 Contributing

### Adding New Examples
1. Create new directory under `src/`
2. Add environment to `platformio.ini`
3. Copy display selection headers from existing example
4. Update this README with your example
5. Submit a pull request

### Reporting Issues
- Hardware problems: Include wiring diagram and photos
- Software problems: Include full error output and environment details
- Feature requests: Describe use case and expected behavior

---

## 📖 Additional Resources

- **GxEPD2 Main Library:** https://github.com/ZinggJM/GxEPD2
- **PlatformIO Documentation:** https://docs.platformio.org/
- **E-Paper Display Guide:** https://learn.adafruit.com/adafruit-eink-display-breakouts
- **Arduino Display Forum:** https://forum.arduino.cc/c/using-arduino/displays/23

---

**Happy coding with e-paper displays! 🎨📟**
