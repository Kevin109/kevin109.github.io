---
title: "TFT Display Configuration Files"
seo_title: "TFT Display Configuration Files"
description: "Browse Rocktech's open-source TFT display configuration files for embedded systems using Rockchip PX30, A64, and other ARM-based SBCs. Includes DTS, kernel drivers, and panel timing examples."
---

# TFT Display Configuration Files for Embedded SBCs
This page provides pre-tested Device Tree Source (DTS) configurations for integrating TFT LCD display modules with popular Rockchip-based Single Board Computers (SBCs), including RK3576, RK3566, RK3568, PX30, A33 and others. It aims to help embedded Linux and Android developers quickly bring up display interfaces in custom or commercial projects.

## ✨ Features

- 📌 Ready-to-use `.dts` and `.dtsi` configuration files
- 🧩 Supports Rocktech TFT LCD modules like RK050HR18, RK070CU01
- 🛠️ Compatible with Android and Linux kernel (4.19/5.10/5.15)
- ✅ Validated on PX30, RK3566 SBC platforms
- 🔧 Easily adaptable to custom SBC designs

---

## 📚 Use Case: Rapid Prototyping

When developing a new product with a Rockchip SoC and TFT LCD, our team typically:
1. Selects a matching Rocktech TFT panel
2. Creates a breakout board for quick bring-up
3. Uses these DTS configs to verify display output before finalizing the SBC design

📂 **GitHub Source (nofollow):**  
<a href="https://github.com/Kevin109/rocktech-tft-display-configs" rel="nofollow">Kevin109/rocktech-tft-display-configs</a>

---

## 📋 Supported Displays

Below are dedicated pages for each display. Each page summarizes configuration methods and links to the GitHub folder.

| Model       | Size  | Resolution | Interface | Learn More |
|-------------|-------|------------|-----------|-------------|
| RK070CU01   | 7.0"  | 1024x600   | LVDS      | [View Details](/tft-config/RK070CU01) |
| RK050HR18   | 5.0"  | 800x480    | RGB       | [View Details](/tft-config/RK050HR18) |
| RK101HI34E  | 10.1" | 1280x800   | LVDS      | [View Details](/tft-config/RK101HI34E) |
| RK050BHD335 | 5.0"  | 720x1280   | MIPI      | [View Details](/tft-config/RK050BHD335) |
| RK035SHV235 | 3.5"  | 320x480    | MIPI      | [View Details](/tft-config/RK035SHV235) |

---

## 🧭 Related Tutorials

- 👉 [RK050BHD335 + PX30 Android Integration](/rk050bhd335-px30-android-setup)
- 👉 [Set Up ADB on Windows for Android SBCs](/setup-adb-on-windows)

---

## 🔗 More from TFT Display

- [More Industrial TFT Displays](https://www.rocktech.com.hk/industrial-tft-displays/)
- [Embedded Board Overview](https://www.rocktech.com.hk/embedded-single-board-computers/)