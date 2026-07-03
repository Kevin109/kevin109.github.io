---
layout: custom
title: "RK3566 Android SBC Guide"
description: "Practical RK3566 Android SBC guide for embedded HMI products, covering display selection, Android BSP, touch integration, ADB debugging, OTA, and production considerations."
date: 2026-07-03
category: sbc-platform
tags: [RK3566, Android SBC, Rockchip, HMI, TFT LCD, Embedded Android]
soc: "Rockchip RK3566"
platform: "RK3566 Android SBC"
os: "Android / Linux"
interface: "MIPI DSI, LVDS, HDMI, Ethernet, USB, UART, I2C, SPI, GPIO, PWM"
---

# RK3566 Android SBC Guide

RK3566 is commonly used in Android smart panels, access control terminals, industrial HMI devices, kiosks, and compact embedded display products. It is a good fit when the product needs a modern touch UI, moderate performance, and practical cost.

## Why RK3566 Is Used in HMI Products

RK3566 offers enough performance for many touch interfaces, WebView applications, Android apps, media playback, networking, and common embedded control tasks. It is often selected when RK3588-level performance is not required.

## Display Integration

Before choosing the TFT LCD, check the actual board connector. RK3566 boards may expose MIPI DSI, LVDS, HDMI, or only selected outputs.

Review:

- Display interface exposed by the board
- Backlight PWM and enable pin
- Touch I2C and interrupt GPIO
- Android rotation requirement
- Kernel and Device Tree support
- Vendor reference panel examples

For display selection, see [How to Choose a TFT LCD for Embedded Linux Projects](/posts/how-to-choose-tft-lcd-for-embedded-linux/).

## Android Development Topics

Typical RK3566 Android SBC work includes BSP customization, launcher setup, kiosk application, ADB debugging, OTA update testing, touch driver integration, and production firmware preparation.

For platform comparison, see [RK3566 vs RK3568 for Embedded HMI Products](/posts/rk3566-vs-rk3568-for-embedded-hmi/).

## Related Guides

- [RK3566 Android SBC Overview](/sbc/rk3566-android-sbc-overview/)
- [Rockchip Android SBC Development Guide](/sbc/rockchip-android-sbc-development/)
- [Android SBC ADB Device Not Found](/sbc/android-sbc-adb-device-not-found/)
