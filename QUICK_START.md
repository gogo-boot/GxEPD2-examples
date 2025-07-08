# 🚀 GxEPD2 Examples - Quick Start Guide

## 30-Second Setup

### 1. Prerequisites Check ✅
- [ ] PlatformIO installed (VS Code extension or CLI)
- [ ] ESP32/ESP8266/Arduino board ready
- [ ] E-paper display connected (see wiring below)
- [ ] USB cable connected

### 2. Configure Your Display (MANDATORY)

**⚠️ The examples will NOT work without this step!**

Edit: `src/GxEPD2_HelloWorld/GxEPD2_display_selection_new_style.h`

Find your display and uncomment the corresponding line:

```cpp
// Most common displays:
#define GxEPD2_DRIVER_CLASS GxEPD2_154_D67    // 1.54" 200x200
//#define GxEPD2_DRIVER_CLASS GxEPD2_213_B73   // 2.13" 250x122  
//#define GxEPD2_DRIVER_CLASS GxEPD2_290_T5D   // 2.9" 296x128
//#define GxEPD2_DRIVER_CLASS GxEPD2_420_T94   // 4.2" 400x300
//#define GxEPD2_DRIVER_CLASS GxEPD2_750_T7    // 7.5" 800x480
```

### 3. Verify Wiring

**ESP32 Standard Wiring:**
```
E-Paper -> ESP32
VCC     -> 3.3V  ⚠️ (NOT 5V!)
GND     -> GND
DIN     -> GPIO23 (MOSI)
CLK     -> GPIO18 (SCK) 
CS      -> GPIO27
DC      -> GPIO14
RST     -> GPIO12
BUSY    -> GPIO13
```

### 4. Upload and Test

```bash
# Upload hello world example
pio run -e hello_world -t upload

# Watch serial output
pio device monitor -e hello_world
```

### 5. Expected Output

**Serial Monitor:**
```
GxEPD2_HelloWorld
Display: GxEPD2_154_D67
setup done
helloWorld
powerOff
```

**Display:**
- Screen should clear (white)
- "Hello World!" text should appear
- Display should go to sleep

## ⚡ If It Doesn't Work

### Quick Fixes

1. **No display output?**
   - Check 3.3V power (measure with multimeter)
   - Verify display selection in code matches your hardware
   - Try different wiring connections

2. **Compilation errors?**
   ```bash
   pio pkg install --force
   pio run -e hello_world -t clean
   pio run -e hello_world
   ```

3. **Upload errors?**
   - Check USB cable (must be data cable, not charge-only)
   - Try different USB port
   - Hold BOOT button during upload (ESP32)

### Debug Commands

```bash
# List connected devices
pio device list

# Verbose build output
pio run -e hello_world -v

# Force clean rebuild
pio run -e hello_world -t clean && pio run -e hello_world
```

## 🎯 Next Steps

Once hello_world works:

1. **Try graphics example:**
   ```bash
   pio run -e gfx_example -t upload
   ```

2. **Explore other examples:**
   ```bash
   pio run -e basic_example -t upload
   pio run -e sd_example -t upload
   pio run -e u8g2_fonts -t upload
   ```

3. **Check the main README.md** for complete documentation

## 🆘 Still Need Help?

- **Hardware issues:** Check your display datasheet
- **Software issues:** See main README.md troubleshooting section
- **Community help:** Arduino Forum displays section

**Success? You're ready to build amazing e-paper projects! 🎨**
