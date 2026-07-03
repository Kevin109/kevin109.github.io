---
layout: custom
title: "SBC Guides"
description: "A practical index of embedded SBC setup notes, Rockchip board references, Android/Linux development guides, ADB usage, network setup, and TFT display integration resources."
permalink: /sbc/
---

# SBC Guides

This section collects practical notes for embedded single-board computer development. The content focuses on Rockchip-based Android and Linux SBCs, display integration, board bring-up, ADB usage, network setup, OTA update testing, and related engineering workflows.

The goal is to provide reusable references for engineers who work with custom SBC hardware, Android/Linux BSPs, TFT LCD modules, touch panels, and embedded HMI products.

## SBC Pages

{% assign sbc_pages = site.pages | where_exp: "page", "page.path contains 'sbc/'" | sort: "title" %}

{% for item in sbc_pages %}
{% unless item.path contains 'index.md' %}
{% unless item.title == nil %}

### [{{ item.title }}]({{ item.url | relative_url }})

{% if item.description %}
{{ item.description }}
{% endif %}

{% if item.soc or item.platform or item.os %}
**Main information:**

{% if item.soc %}
- SoC: {{ item.soc }}
{% endif %}
{% if item.platform %}
- Platform: {{ item.platform }}
{% endif %}
{% if item.os %}
- Operating system: {{ item.os }}
{% endif %}
{% if item.interface %}
- Main interfaces: {{ item.interface }}
{% endif %}
{% endif %}

{% if item.tags %}
<div class="post-tags">
  <span class="post-tags-label">Tags:</span>
  {% for tag in item.tags %}
    <span class="post-tag">{{ tag }}</span>
  {% endfor %}
</div>
{% endif %}

---

{% endunless %}
{% endunless %}
{% endfor %}

## What This Section Covers

Embedded SBC development usually requires both hardware and software work. A board may boot successfully, but display, touch, Wi-Fi, Ethernet, UART, GPIO, backlight, audio, camera, or OTA update functions still need to be configured and tested.

This section is designed to collect practical guides related to:

- Android SBC setup
- Linux SBC setup
- Rockchip board bring-up
- TFT LCD display integration
- Device Tree configuration
- ADB usage
- Network configuration
- OTA update testing
- GPIO and peripheral debugging
- BSP customization
- Production test preparation

These guides are not intended to replace the official BSP documentation. Instead, they provide practical engineering notes that are easier to reference during real board development.

## Platform Selection Guides

- [Android SBC vs Linux SBC for Industrial Display Products](/posts/android-sbc-vs-linux-sbc-for-industrial-display/)
- [RK3566 vs RK3568 for Embedded HMI Products](/posts/rk3566-vs-rk3568-for-embedded-hmi/)
- [How to Choose a TFT LCD for Embedded Linux Projects](/posts/how-to-choose-tft-lcd-for-embedded-linux/)

## Chip and Board Platform Guides

- [PX30 Android SBC Display Guide](/sbc/px30-android-sbc-display-guide/)
- [RK3566 Android SBC Guide](/sbc/rk3566-android-sbc-guide/)
- [RK3568 LVDS and MIPI Display Guide](/sbc/rk3568-lvds-mipi-display-guide/)
- [RK3576 Display Configuration Guide](/sbc/rk3576-display-configuration-guide/)
- [RK3588 Embedded Display Integration](/sbc/rk3588-embedded-display-integration/)
- [Allwinner A64 RGB LCD Configuration](/sbc/allwinner-a64-rgb-lcd-configuration/)
- [Android SBC ADB Device Not Found](/sbc/android-sbc-adb-device-not-found/)

## Common SBC Development Topics

### Board Bring-Up

Board bring-up is the first stage of custom SBC development. Engineers need to confirm that the CPU, DDR, storage, PMIC, bootloader, kernel, display, and basic peripherals are working correctly.

Typical bring-up checks include:

- Power rail verification
- Serial console output
- Bootloader loading
- DDR initialization
- eMMC or SD card detection
- Kernel boot log
- Root filesystem mount
- Ethernet or Wi-Fi connection
- USB device detection
- Display output
- Touch input
- Backlight control
- GPIO status

A stable bring-up process helps identify whether an issue is caused by hardware design, bootloader configuration, kernel drivers, or user-space software.

### Android SBC Development

Android SBCs are commonly used in smart control panels, HMI devices, access control terminals, kiosks, digital signage players, medical devices, and smart appliance interfaces.

Android development on an SBC may involve:

- AOSP or vendor Android BSP
- Device Tree modification
- Display timing configuration
- Touch panel driver integration
- Camera HAL configuration
- Wi-Fi and Bluetooth module setup
- Audio codec configuration
- Launcher or kiosk application
- OTA update package testing
- ADB debugging
- Factory reset and recovery testing

For Android-based products, display and touch stability are especially important because the screen is usually the main user interface.

### Linux SBC Development

Linux SBCs are often used in gateways, control terminals, data collection devices, industrial automation systems, laboratory instruments, and custom embedded computers.

Linux SBC development may involve:

- U-Boot configuration
- Kernel driver integration
- Device Tree setup
- Buildroot or Yocto image generation
- Debian or Ubuntu testing
- Serial communication
- Ethernet and network services
- GPIO control
- PWM and backlight control
- Systemd services
- Remote update strategy
- Long-time stability testing

Compared with Android, Linux usually gives developers more direct access to system services and hardware interfaces. This makes it suitable for industrial and hardware-oriented products.

## Rockchip SBC Notes

Rockchip SoCs are widely used in Android and Linux SBC products because they provide a practical balance of performance, display support, multimedia capability, software ecosystem, and cost.

Common Rockchip platforms used in embedded SBCs include:

- PX30
- RK3566
- RK3568
- RK3576
- RK3588

These platforms can support different product levels, from small HMI panels to high-performance edge devices.

For Rockchip SBC development, engineers often need to work with:

- U-Boot
- Linux kernel
- Android BSP
- Device Tree files
- RKDevTool or upgrade tools
- ADB
- Serial console
- Display controller configuration
- MIPI DSI, LVDS, RGB, HDMI, or eDP output
- GPIO and PWM configuration
- Wi-Fi, Bluetooth, Ethernet, USB, UART, I2C, SPI

## Display Integration on SBCs

Display integration is one of the most common tasks in embedded SBC projects. A product may use a 5-inch, 7-inch, 10.1-inch, 12.1-inch, or 15.6-inch TFT LCD depending on the application.

Common display interfaces include:

- MIPI DSI
- LVDS
- RGB
- HDMI
- eDP

A display configuration usually requires:

- Correct panel timing
- Correct interface selection
- Power sequence control
- Reset GPIO
- Backlight enable GPIO
- PWM brightness control
- Touch panel driver
- Screen rotation
- Coordinate mapping
- Long-time display stability testing

Display issues may appear as a black screen, white screen, flickering image, wrong colors, incorrect resolution, unstable backlight, reversed touch coordinates, or failed initialization. These problems often require checking both the hardware schematic and the software configuration.

## ADB and Debugging

ADB is an important tool for Android SBC development. It allows engineers to connect to the device, check logs, install applications, push files, pull files, reboot the system, and test OTA updates.

Common ADB operations include:

    adb devices
    adb shell
    adb logcat
    adb push localfile /sdcard/
    adb pull /sdcard/file .
    adb install app.apk
    adb reboot
    adb reboot recovery

For production projects, ADB may be disabled or restricted for security reasons. During development, however, it is one of the most useful debugging tools.

## Network Setup

Network access is important for both Android and Linux SBCs. Engineers often need to find the board IP address, test Ethernet, connect Wi-Fi, configure static IP, or access the board remotely.

Useful checks include:

    ip addr
    ifconfig
    ping 8.8.8.8
    ping google.com
    route -n
    cat /etc/resolv.conf

On Android systems, network status can also be checked through ADB shell or system settings.

Network problems may be caused by missing drivers, wrong MAC address, DHCP failure, DNS failure, incorrect gateway, cable problems, or switch configuration.

## OTA and Firmware Update

Firmware update support is important for embedded products after deployment. Android products may use OTA packages, recovery mode, or vendor upgrade tools. Linux products may use A/B partitions, SWUpdate, RAUC, Mender, or custom update scripts.

An update strategy should consider:

- Power failure protection
- Rollback support
- Version control
- Signature verification
- Storage partition layout
- Recovery method
- Factory reset behavior
- Remote update process
- User data preservation

For commercial products, update reliability is as important as the original firmware image.

## Recommended Reading

- [TFT Config Index](/tft-config/)
- [Technical Posts](/posts/)
- [GitHub Display Config](/github-display-config)
- [RK050BHD335 PX30 Android Setup](/rk050bhd335-px30-android-setup)
- [Get IP of SBC](/get-ip-of-SBC)
- [Setup ADB on Windows](/setup-adb-on-windows)
- [Upgrade Android OTA via ADB](/upgrade-android-ota-via-adb)

## GitHub Repository

The related TFT display configuration files are maintained in the GitHub repository:

[rocktech-tft-display-configs](https://github.com/Kevin109/rocktech-tft-display-configs)

This repository includes example Device Tree configuration files, panel notes, and display integration references for Rockchip-based embedded SBC projects.

## Notes for Developers

The information in this section is based on practical embedded SBC development workflows. Actual implementation may vary depending on the SoC, board design, BSP version, kernel version, Android version, Linux distribution, display panel, touch controller, and hardware revision.

Before applying any configuration to a production device, always compare it with:

- The SBC schematic
- The SoC datasheet or technical reference manual
- The LCD panel datasheet
- The touch controller datasheet
- The bootloader source code
- The kernel Device Tree
- The Android or Linux BSP
- The production test requirements

A stable embedded SBC product depends on the complete system design, including hardware, software, enclosure, power, thermal behavior, display integration, and long-term maintenance.
