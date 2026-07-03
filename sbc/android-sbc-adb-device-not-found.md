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

## Check ADB Authorization

If the board appears in `adb devices` as `unauthorized`, the USB link and driver are already working. The problem is authorization. On a normal Android product, a prompt appears on the device asking whether to allow USB debugging from the connected computer. Accept the prompt and optionally select always allow.

For embedded products without a visible launcher or with a custom kiosk app, the prompt may be hidden behind the application. Temporarily boot to a development launcher or enable a debug build that pre-authorizes the development computer. Do not ship production firmware with open ADB unless the product security model allows it.

## Check USB Mode on the SBC

Some Android SBCs have a USB OTG port that can work as host or device. ADB requires device mode. If the board is in host mode, the PC will not see it as an Android device.

Review:

- OTG ID pin state
- USB Type-C role configuration if used
- Device Tree USB controller mode
- Kernel USB gadget support
- Cable type and adapter direction

If the same port can power USB peripherals, that does not guarantee it can expose ADB to a PC. Check the board manual for the correct debug port.

## Vendor ID and udev Rules on Linux

On Linux hosts, ADB may fail because the user does not have permission to access the USB device. Add the correct vendor ID to udev rules, reload rules, and reconnect the board. Rockchip and other vendors may use different IDs depending on boot mode and firmware state.

Basic checks:

```bash
lsusb
adb kill-server
adb start-server
adb devices
```

If `lsusb` sees the board but ADB does not, the issue is usually permissions, vendor ID, or ADB interface exposure.

## Firmware-Level Causes

In production firmware, ADB may be intentionally disabled. This can happen through system properties, build type, init scripts, USB configuration, or security policy. A board may expose ADB in engineering firmware and hide it in user firmware.

Ask these questions:

- Is the build `user`, `userdebug`, or `eng`?
- Is USB debugging enabled by default?
- Is the USB function set to `adb` or only `mtp`?
- Does the product disable developer options?
- Is the USB port configured as host only?

## A Practical Debug Flow

Use this order:

1. Confirm the cable and correct USB port.
2. Confirm the board boots normally.
3. Check Device Manager or `lsusb`.
4. Install or fix the driver.
5. Restart the ADB server.
6. Handle authorization.
7. Check firmware USB configuration.
8. Try Wi-Fi ADB only after network access is confirmed.

This prevents wasting time on firmware changes when the real cause is a charge-only cable or missing Windows driver.

## Related Guides

- [Upgrade Android OTA File via ADB](/upgrade-android-ota-via-adb)
- [Rockchip Android SBC Development Guide](/sbc/rockchip-android-sbc-development/)
- [Android SBC vs Linux SBC for Industrial Display Products](/posts/android-sbc-vs-linux-sbc-for-industrial-display/)
