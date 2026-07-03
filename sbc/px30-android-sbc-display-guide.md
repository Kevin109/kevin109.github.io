---
layout: custom
title: "PX30 Android SBC Display Guide"
description: "Guide to PX30 Android SBC display integration, including MIPI DSI, RGB, panel timing, backlight, touch, Device Tree, Android rotation, and common debugging steps."
date: 2026-07-03
category: sbc-platform
tags: [PX30, Android SBC, Rockchip, MIPI DSI, RGB, TFT LCD, HMI]
soc: "Rockchip PX30"
platform: "PX30 Android SBC"
os: "Android / Linux"
interface: "MIPI DSI, RGB, USB, Ethernet, UART, I2C, GPIO, PWM"
---

# PX30 Android SBC Display Guide

PX30 is a practical Rockchip platform for compact Android SBC products such as smart home panels, access terminals, small HMI devices, and embedded control screens. It is often paired with MIPI DSI or RGB TFT LCD panels.

## Display Planning

Before choosing a panel, confirm which display interface the PX30 board exposes. Some boards expose MIPI DSI, some expose RGB, and some route only one interface to the display connector.

Check:

- MIPI DSI lane count
- RGB data width if used
- Backlight PWM and enable GPIO
- Touch I2C bus and interrupt GPIO
- LCD power rails
- FPC connector pinout

## MIPI DSI Bring-Up

PX30 MIPI panels may need panel initialization commands, reset timing, lane setup, and exact timing values. If the screen stays black, debug power and reset first, then DSI lanes and panel commands.

Related guide: [PX30 MIPI Display Debugging Guide](/posts/px30-mipi-display-debugging/).

## Android Integration

For Android products, display bring-up is not finished until rotation, touch mapping, brightness control, suspend/resume, boot logo, and OTA update screens are tested.

Useful related pages:

- [Rockchip Android Display Rotation Configuration](/tft-config/rockchip-android-display-rotation-configuration/)
- [RK050BHD335 PX30 Android Setup](/rk050bhd335-px30-android-setup)
- [Set up ADB on Windows](/setup-adb-on-windows)

## Related Guides

- [MIPI vs LVDS vs RGB Display Interface](/posts/mipi-vs-lvds-vs-rgb-display-interface/)
- [How to Choose a TFT LCD for Embedded Linux Projects](/posts/how-to-choose-tft-lcd-for-embedded-linux/)
- [SBC Guides](/sbc/)
