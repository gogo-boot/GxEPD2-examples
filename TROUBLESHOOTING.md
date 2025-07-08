# 🐛 GxEPD2 Examples - Troubleshooting Guide

## 🚨 Emergency Checklist

**Before diving deep, check these common issues:**

- [ ] Display selection configured in code? (See [DISPLAY_CONFIG.md](DISPLAY_CONFIG.md))
- [ ] 3.3V power supply? (NOT 5V!)
- [ ] Wiring matches code pin definitions?
- [ ] PlatformIO dependencies installed?
- [ ] Correct board selected in platformio.ini?

## 🔧 Build & Compilation Issues

### ❌ "No such file or directory" Errors

**Symptoms:**
```
fatal error: GxEPD2_154_D67.h: No such file or directory
```

**Solutions:**
```bash
# 1. Update dependencies
pio pkg update

# 2. Force reinstall
pio pkg install --force

# 3. Clean and rebuild
pio run -e hello_world -t clean
pio run -e hello_world
```

### ❌ "Multiple definition" Errors

**Symptoms:**
```
multiple definition of `display'
```

**Solutions:**
1. **Check display selection files** - only one display should be uncommented
2. **Remove duplicate includes** in your code
3. **Clean build:**
   ```bash
   pio run -t clean
   ```

### ❌ "Platform not found" Errors

**Symptoms:**
```
Error: Unknown platform 'espressif32'
```

**Solutions:**
```bash
# Install platform
pio platform install espressif32

# Update platforms
pio platform update
```

### ❌ Library Version Conflicts

**Symptoms:**
```
Library dependency graph:
Error: Dependency 'adafruit/Adafruit GFX Library' not found
```

**Solutions:**
```bash
# Fix dependencies
pio pkg install --library "adafruit/Adafruit GFX Library@^1.11.9"

# Or update platformio.ini
[env]
lib_deps = 
    adafruit/Adafruit GFX Library@^1.11.9
```

## 🔌 Upload & Connection Issues

### ❌ Upload Failed / Device Not Found

**Symptoms:**
```
Error: Please specify `upload_port` for environment
```

**Solutions:**
```bash
# 1. List available ports
pio device list

# 2. Specify port manually
pio run -e hello_world -t upload --upload-port /dev/ttyUSB0

# 3. Try different USB cable (data cable, not charge-only)
```

### ❌ ESP32 Boot Mode Issues

**Symptoms:**
- Upload starts but fails
- Device resets during upload
- "Timed out waiting for packet header" error

**Solutions:**
1. **Hold BOOT button** during upload initiation
2. **Check reset button** - don't press during upload
3. **Try different upload speed:**
   ```ini
   [env:hello_world]
   upload_speed = 115200  ; Try slower speed
   ```

### ❌ Permission Denied (Linux/Mac)

**Symptoms:**
```
Permission denied: '/dev/ttyUSB0'
```

**Solutions:**
```bash
# Add user to dialout group
sudo usermod -a -G dialout $USER

# Or use sudo (not recommended)
sudo pio run -e hello_world -t upload
```

## 📟 Display Hardware Issues

### ❌ Nothing Appears on Display

**Diagnostic Steps:**

1. **Check power consumption:**
   ```bash
   # Should show current draw during refresh
   pio device monitor -e hello_world
   ```

2. **Verify 3.3V power:**
   - Measure VCC pin with multimeter
   - Check current capacity (min 500mA)
   - ESP32 3.3V pin may not provide enough current

3. **Test with minimal code:**
   ```cpp
   void setup() {
     Serial.begin(115200);
     display.init();
     display.fillScreen(GxEPD_WHITE);
     display.display();
     Serial.println("Display refresh complete");
   }
   ```

### ❌ Display Shows Garbage/Artifacts

**Possible Causes & Solutions:**

1. **Wrong display driver:**
   - Double-check model number on display back
   - Try similar size displays in configuration

2. **Power supply issues:**
   - Use external 3.3V regulator
   - Add capacitors: 100µF + 10µF ceramic
   
3. **Wiring problems:**
   - Check continuity with multimeter
   - Ensure no loose connections
   - Try shorter wires

4. **SPI timing issues:**
   ```cpp
   // Try slower SPI speed
   display.epd2.selectSPI(settings_slow);
   ```

### ❌ Display Partially Updates

**Symptoms:**
- Only part of screen updates
- Horizontal/vertical lines
- Faded appearance

**Solutions:**
1. **Check BUSY pin connection** - critical for timing
2. **Increase power supply capacity**
3. **Check temperature** - displays work best 0-40°C
4. **Try full refresh:**
   ```cpp
   display.setFullWindow();
   display.fillScreen(GxEPD_WHITE);
   display.display();
   ```

## 💻 Software & Logic Issues

### ❌ Serial Monitor Shows Nothing

**Check:**
```cpp
// Ensure Serial.begin() is called
void setup() {
  Serial.begin(115200);
  delay(1000);  // Wait for serial connection
  Serial.println("Starting...");
}
```

**PlatformIO Monitor:**
```bash
# Correct monitor command
pio device monitor -e hello_world -b 115200
```

### ❌ Code Runs But Display Doesn't Update

**Debug Steps:**
```cpp
void setup() {
  Serial.begin(115200);
  
  // Check if display initializes
  if (!display.init()) {
    Serial.println("Display init failed!");
    return;
  }
  
  Serial.println("Display initialized");
  
  // Add debug prints
  display.fillScreen(GxEPD_WHITE);
  Serial.println("Screen filled");
  
  display.display();
  Serial.println("Display updated");
}
```

### ❌ Memory Issues (ESP32)

**Symptoms:**
```
Guru Meditation Error: Core 1 panic'ed (LoadProhibited)
```

**Solutions:**
1. **Enable PSRAM:**
   ```ini
   [env:hello_world]
   build_flags = 
     ${env.build_flags}
     -DBOARD_HAS_PSRAM
   ```

2. **Use paged drawing:**
   ```cpp
   // Instead of direct drawing, use callbacks
   display.setFullWindow();
   display.firstPage();
   do {
     // Draw content here
   } while (display.nextPage());
   ```

## 📊 Performance Issues

### ❌ Slow Display Updates

**Optimizations:**
1. **Use partial updates:**
   ```cpp
   display.setPartialWindow(x, y, w, h);
   display.display(true);  // Partial update
   ```

2. **Optimize drawing:**
   ```cpp
   // Group operations
   display.fillScreen(GxEPD_WHITE);
   display.setTextColor(GxEPD_BLACK);
   display.print("Text");
   display.display();  // Single update
   ```

### ❌ Memory Usage Too High

**Solutions:**
1. **Use smaller fonts**
2. **Reduce image sizes**
3. **Use PROGMEM for large data:**
   ```cpp
   const uint8_t myBitmap[] PROGMEM = { ... };
   ```

## 🔍 Advanced Debugging

### Enable Debug Output

```cpp
// Add to your code
#define ENABLE_GxEPD2_display 1
```

### PlatformIO Debug Build

```bash
# Verbose build
pio run -e hello_world -v

# Debug build flags
[env:hello_world]
build_type = debug
build_flags = 
  ${env.build_flags}
  -DCORE_DEBUG_LEVEL=5
  -DDEBUG_ESP_PORT=Serial
```

### Hardware Testing

```cpp
// Test SPI communication
void testSPI() {
  SPI.begin();
  pinMode(EPD_CS, OUTPUT);
  
  digitalWrite(EPD_CS, LOW);
  SPI.transfer(0x00);  // Test command
  digitalWrite(EPD_CS, HIGH);
  
  Serial.println("SPI test complete");
}
```

## 📞 Getting Help

### Information to Include

When asking for help, provide:

1. **Hardware setup:**
   - Board type (ESP32, ESP8266, etc.)
   - Display model number
   - Wiring diagram/photo
   - Power supply details

2. **Software details:**
   - PlatformIO version: `pio --version`
   - Complete error messages
   - Code modifications made
   - Which example you're using

3. **Environment:**
   - Operating system
   - USB cable type
   - Any external components

### Useful Commands

```bash
# System info
pio --version
pio system info

# Project info
pio project config
pio pkg list

# Device info
pio device list
pio device monitor -e hello_world --echo
```

## 🔗 Additional Resources

- **GxEPD2 Library Issues:** https://github.com/ZinggJM/GxEPD2/issues
- **PlatformIO Support:** https://community.platformio.org/
- **Arduino Forums:** https://forum.arduino.cc/c/using-arduino/displays/23
- **ESP32 Troubleshooting:** https://docs.espressif.com/projects/esp-idf/en/latest/esp32/

---

**Still stuck? Check [QUICK_START.md](QUICK_START.md) for basic setup or [DISPLAY_CONFIG.md](DISPLAY_CONFIG.md) for display-specific help.**
