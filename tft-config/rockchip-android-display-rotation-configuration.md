---
title: "Rockchip Android Display Rotation Configuration"
description: "Guide to Rockchip Android display rotation configuration for embedded TFT LCD products, covering panel orientation, Android system rotation, touch mapping, launcher behavior, and common mistakes."
date: 2026-07-03
category: display-configuration
tags: [Rockchip, Android, Display Rotation, TFT LCD, Touch Panel, Embedded HMI]
---

# Rockchip Android Display Rotation Configuration

Many embedded Android products use portrait TFT panels in a landscape-oriented system, or landscape panels in a portrait enclosure. On Rockchip Android SBCs, display rotation must be handled together with touch mapping, launcher layout, boot logo, and application orientation.

## Identify the Real Panel Orientation

Start with the panel datasheet. Some panels are physically portrait, such as 720x1280, while the product UI may be landscape. Others are landscape, such as 1024x600, but may be mounted vertically in the enclosure.

Record:

- Native resolution
- Physical mounting direction
- Desired UI orientation
- Touch coordinate direction
- Boot logo orientation

## Android Rotation Areas

Depending on BSP version, rotation may be configured in several places:

- Android system properties
- Display framework configuration
- Launcher or application orientation
- SurfaceFlinger or vendor display settings
- Touch input calibration
- Boot animation and logo resources

Changing only the app orientation is not enough if touch coordinates or system UI remain wrong.

## Touch Mapping

Touch is the most common rotation mistake. The image may rotate correctly while touch input remains swapped or inverted.

Check:

- Touch controller driver
- Input device coordinate range
- X/Y swap setting
- X or Y inversion
- Android input calibration file if used
- Whether the touch panel was bonded in the same direction as the LCD

## Testing Checklist

Test rotation during:

- Boot logo
- Android boot animation
- Launcher
- Main application
- Touch input
- Sleep and wake
- OTA update screen if used

## Related Guides

- [Rockchip Android SBC Development Guide](/sbc/rockchip-android-sbc-development/)
- [RK050BHD335 PX30 Android Setup](/rk050bhd335-px30-android-setup)
- [TFT Config Index](/tft-config/)
