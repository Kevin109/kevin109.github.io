---
layout: custom
title: "Android SBC ADB Device Not Found"
description: "Troubleshooting guide for Android SBC ADB device not found problems, covering USB cable, drivers, USB debugging, vendor ID, adb server reset, Wi-Fi ADB, and production firmware settings."
date: 2026-07-03
category: sbc-debugging
tags: [Android SBC, ADB, USB Debugging, Rockchip, Windows Driver, Embedded Android]
soc: "Rockchip / Android SBC"
platform: "Android embedded SBC"
os: "Android"
interface: "USB, Wi-Fi, ADB"
---

# Android SBC ADB Device Not Found

ADB is one of the most useful tools when debugging Android SBC products. If `adb devices` does not show the board, the problem is usually USB wiring, Windows driver installation, USB debugging settings, ADB authorization, firmware configuration, or a stale ADB server.

## Start With the Physical Connection

Check the simple items first:

- Use a data-capable USB cable
- Try another USB port
- Confirm the board is powered correctly
- Confirm the USB connector supports device mode, not only host mode
- Avoid unpowered USB hubs during first debugging

Some SBCs have multiple USB ports. Only one may support ADB device mode.

## Check Windows Driver

On Windows, a missing or wrong driver is common. Install the correct Android USB or Rockchip driver, then check Device Manager. If the device appears as unknown, reinstall the driver and reconnect the board.

For setup steps, see [Set up ADB on Windows](/setup-adb-on-windows).

## Enable USB Debugging

On development firmware, USB debugging must be enabled. Some production firmware disables ADB for security. If the display is available, enable developer options and USB debugging. If there is no display, ask the BSP provider whether ADB is enabled by default.

## Reset the ADB Server

When the driver is correct but the device still does not appear, restart ADB:

```bash
adb kill-server
adb start-server
adb devices
```

If the device is listed as unauthorized, confirm the authorization prompt on the device screen.

## Use Wi-Fi ADB When USB Is Not Practical

If USB ADB is not available but the device is on the network, use the device IP address and connect over Wi-Fi ADB if the firmware supports it.

Related guide: [How to Get the IP Address of Your SBC or Smart Device](/get-ip-of-SBC).

## Related Guides

- [Upgrade Android OTA File via ADB](/upgrade-android-ota-via-adb)
- [Rockchip Android SBC Development Guide](/sbc/rockchip-android-sbc-development/)
- [Android SBC vs Linux SBC for Industrial Display Products](/posts/android-sbc-vs-linux-sbc-for-industrial-display/)
