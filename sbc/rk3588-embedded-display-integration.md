---
layout: custom
title: "RK3588 Embedded Display Integration"
description: "Guide to RK3588 embedded display integration for high-performance Android and Linux products, covering MIPI DSI, HDMI, eDP, multi-display, touch, backlight, and production testing."
date: 2026-07-03
category: sbc-platform
tags: [RK3588, Rockchip, Embedded Display, Android SBC, Linux SBC, HDMI, eDP, MIPI DSI]
soc: "Rockchip RK3588"
platform: "RK3588 embedded SBC"
os: "Android / Linux"
interface: "MIPI DSI, HDMI, eDP, USB, Ethernet, PCIe, I2C, GPIO, PWM"
---

# RK3588 Embedded Display Integration

RK3588 is used in high-performance embedded products that need stronger CPU, GPU, multimedia, AI, camera, storage, or multi-display capability. It can be suitable for advanced HMI systems, digital signage, AI terminals, medical devices, and edge computing products with display output.

## Display Planning

RK3588 boards may expose MIPI DSI, HDMI, eDP, or multiple display outputs. The actual capability depends on board routing and BSP support.

Check:

- Required display count
- Display resolution and refresh rate
- HDMI, eDP, or MIPI DSI connector availability
- Touch input path
- GPU and video workload
- Android or Linux display framework support

## Multi-Display Considerations

If the product uses more than one display, test independent resolution, orientation, touch association, boot behavior, and application window placement. Multi-display bugs are often framework-level issues, not only kernel display issues.

## TFT LCD Integration

For internal TFT LCDs, the same basics still apply: panel timing, power sequence, backlight, reset GPIO, and touch mapping must match the hardware.

Related guides:

- [Device Tree Panel Timing Explanation](/tft-config/device-tree-panel-timing-explanation/)
- [PWM Backlight Configuration in Linux Device Tree](/tft-config/pwm-backlight-configuration-linux-device-tree/)
- [Rockchip Android Display Rotation Configuration](/tft-config/rockchip-android-display-rotation-configuration/)

## Related Guides

- [Rockchip Android SBC Development Guide](/sbc/rockchip-android-sbc-development/)
- [Android SBC vs Linux SBC for Industrial Display Products](/posts/android-sbc-vs-linux-sbc-for-industrial-display/)
- [SBC Guides](/sbc/)
