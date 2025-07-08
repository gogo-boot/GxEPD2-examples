# GxEPD2 Examples - Example Selection Guide

## 🎯 Which Example Should I Start With?

### 🚀 Absolute Beginner
**Start here:** `hello_world`
- Simplest possible example
- Just displays "Hello World!" text
- Perfect for testing your setup
- **Command:** `pio run -e hello_world -t upload`

### 🖼️ Want to Show Graphics?
**Try:** `gfx_example`
- Text with different fonts
- Basic shapes and lines  
- Bitmap images
- **Command:** `pio run -e gfx_example -t upload`

### 🔧 Need Full Feature Demo?
**Use:** `basic_example`
- Comprehensive GxEPD2 features
- Multiple display modes
- Various text and graphics
- **Command:** `pio run -e basic_example -t upload`

## 📱 Example Categories

### Core Display Examples
| Example | Purpose | Difficulty |
|---------|---------|------------|
| `hello_world` | Test basic functionality | ⭐ Beginner |
| `basic_example` | Full feature demonstration | ⭐⭐ Intermediate |
| `gfx_example` | Graphics and text rendering | ⭐⭐ Intermediate |
| `not_paged` | Direct drawing (high memory) | ⭐⭐ Intermediate |
| `paged_callback` | Memory-efficient drawing | ⭐⭐⭐ Advanced |

### Storage & Data Examples
| Example | Purpose | Requirements |
|---------|---------|--------------|
| `sd_example` | SD card image loading | SD card module |
| `spiffs_example` | Internal flash storage | ESP32/ESP8266 |
| `serial_flash_example` | External flash storage | Serial flash chip |

### Advanced Features
| Example | Purpose | Special Hardware |
|---------|---------|------------------|
| `multi_display` | Multiple e-paper displays | 2+ displays |
| `rotary_callback` | Rotary encoder interface | Rotary encoder |
| `u8g2_fonts` | Advanced font rendering | None |
| `mixed_test` | Complex display testing | None |

## 🛠️ Hardware-Specific Examples

### Arduino Uno/Nano Users
**Recommended:** `sd_avr_example`
- Optimized for AVR memory constraints
- Works with Arduino Uno/Nano
- **Command:** `pio run -e sd_avr_example -t upload`

### ESP8266 Users  
**Try any example with:** `*_esp8266` suffix
- Example: `pio run -e hello_world_esp8266 -t upload`
- Optimized for ESP8266 memory/pins

### ESP32-S3 Users
**Use:** `*_esp32s3` variants
- Example: `pio run -e hello_world_esp32s3 -t upload`  
- Takes advantage of S3 features

## 🎨 What Each Example Demonstrates

### `hello_world` - The Basics
```cpp
// Shows:
display.init();           // Initialize display  
display.fillScreen(GxEPD_WHITE);
display.setTextColor(GxEPD_BLACK);
display.print("Hello World!");
display.display();        // Update screen
```

### `gfx_example` - Graphics & Text
```cpp
// Shows:
display.drawLine(x1, y1, x2, y2, color);
display.drawRect(x, y, w, h, color);
display.drawBitmap(x, y, bitmap, w, h, color);
display.setFont(&FreeMonoBold9pt7b);
display.setTextSize(2);
```

### `basic_example` - Full Features
```cpp
// Shows:
display.setRotation(rotation);
display.setPartialWindow(x, y, w, h);
display.display(partial_update);
display.hibernate();
```

### `paged_callback` - Memory Management
```cpp
// Shows:
display.setFullWindow();
display.firstPage();
do {
  // Draw everything here - called multiple times
  drawContent();
} while (display.nextPage());
```

## 🔄 Example Progression Path

### Learning Path
1. **`hello_world`** - Get basic display working
2. **`gfx_example`** - Learn graphics functions  
3. **`basic_example`** - Understand full API
4. **`paged_callback`** - Master memory management
5. **Storage examples** - Add data persistence
6. **Advanced examples** - Special features

### Project Development Path
1. **Start with closest example** to your project needs
2. **Copy and modify** the example code
3. **Test incrementally** as you add features
4. **Use paged drawing** for complex graphics

## 🚨 Common Mistakes to Avoid

### ❌ Wrong Starting Example
- **Don't start with complex examples** like `mixed_test`
- **Always begin with `hello_world`** to verify setup

### ❌ Skipping Configuration  
- **Must configure display type** in each example
- **Check wiring matches** the example's pin definitions

### ❌ Memory Issues
- **Large images need paged drawing** (`paged_callback`)
- **Arduino Uno has limited RAM** - use AVR examples

## 🎯 Quick Selection Guide

**Just want it to work?** → `hello_world`

**Want to show images?** → `gfx_example` 

**Using SD card?** → `sd_example`

**Arduino Uno/Nano?** → `sd_avr_example`

**Multiple displays?** → `multi_display`

**Need advanced fonts?** → `u8g2_fonts`

**Want everything?** → `basic_example`

---

**Remember:** Every example requires display configuration in `GxEPD2_display_selection_new_style.h` before it will work!
