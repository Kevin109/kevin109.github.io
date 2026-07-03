---
title: "TFT & SBC Integration Notes"
description: "Technical notes for TFT display configuration, Rockchip SBC development, Linux LCD debugging, Android OTA updates, ADB setup, and embedded board integration."
---

# TFT & SBC Integration Notes

Welcome to the official documentation hub for embedded display and SBC solutions. This site includes configuration guides, hardware integration tutorials, and performance optimization tips for our Rockchip-based SBCs and TFT LCD modules.

---

## 📘 Sections

### 🧠 Single Board Computers (SBC)

Explore Rockchip-based SBC development tutorials, covering bootloader setup, UART access, OTA upgrades, and IP configuration.

#### 🔌 [Set up ADB on Windows](/setup-adb-on-windows)  
_Set up ADB for debugging and firmware updates over USB or Wi-Fi._

#### 📦 [Upgrade Android OTA via ADB](/upgrade-android-ota-via-adb)  
_Install `update.zip` OTA packages directly from your PC._

#### 🌐 [Find Device IP Address](/get-ip-of-SBC)  
_Get your SBC or smart device IP for ADB over Wi-Fi or SSH._

#### 🌐 [Customize a Single Board Computer](/how-to-customize-single-board-computer)  
_Get your SBC or smart device IP for ADB over Wi-Fi or SSH._

---

### 📺 TFT LCD Displays

Learn how to configure and integrate TFT panels with embedded platforms, including LVDS/MIPI settings and optical bonding methods.

#### 🧰 [Display Configuration Index](/github-display-config)  
_View all Rocktech TFT panel configurations (DTS, drivers, overlays)._

#### 🛠️ [RK050BHD335 + PX30 Integration Guide](/rk050bhd335-px30-android-setup)  
_A hands-on tutorial showing how to drive a 5" MIPI display on PX30 SBC using fly-wire adapter._

---

## Selection Guides

These guides help engineers choose display interfaces, TFT panel sizes, and SBC platforms before starting hardware integration.

- [MIPI vs LVDS vs RGB Display Interface](/posts/mipi-vs-lvds-vs-rgb-display-interface/)
- [How to Choose a TFT LCD for Embedded Linux Projects](/posts/how-to-choose-tft-lcd-for-embedded-linux/)
- [5 Inch vs 7 Inch TFT Display for HMI Products](/posts/5-inch-vs-7-inch-tft-display-for-hmi/)
- [Android SBC vs Linux SBC for Industrial Display Products](/posts/android-sbc-vs-linux-sbc-for-industrial-display/)
- [RK3566 vs RK3568 for Embedded HMI Products](/posts/rk3566-vs-rk3568-for-embedded-hmi/)

---

## 🧰 Resources

- [GitHub Repository](https://github.com/Kevin109/rocktech-tft-display-configs)
- [Rocktech Official Website](https://www.rocktech.com.hk)
- [Factory Overview](https://www.rocktech.com.hk/factory-overview/)

---

## 🛠 Contributions

We welcome contributions and suggestions. Feel free to submit a pull request or open an issue for bugs, updates, or additional topics you'd like to see.

---

> **Note:** This documentation is optimized for hardware engineers, embedded developers, and product designers working on smart control panels, industrial interfaces, and custom display integrations.
