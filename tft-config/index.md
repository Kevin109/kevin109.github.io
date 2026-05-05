---
layout: custom
title: "TFT Config Index"
description: "A practical index of TFT LCD display configuration files, panel notes, Device Tree examples, and embedded SBC display integration references."
permalink: /tft-config/
---

# TFT Config Index

This section collects TFT LCD display configuration references for embedded SBC development. The goal is to help engineers quickly find panel information, interface notes, Device Tree examples, and related display bring-up guides for Rockchip-based Android and Linux platforms.

These configuration notes are mainly focused on practical display integration work, including LVDS, MIPI DSI, RGB, backlight control, panel timing, touch panel setup, and board-level display debugging.

## Display Configuration Files

{% assign tft_pages = site.pages | where_exp: "page", "page.path contains 'tft-config/'" | sort: "title" %}

{% for panel in tft_pages %}
{% unless panel.path contains 'index.md' %}
{% unless panel.title == nil %}

### [{{ panel.title }}]({{ panel.url | relative_url }})

{% if panel.description %}
{{ panel.description }}
{% endif %}

{% if panel.size or panel.resolution or panel.interface %}
**Main specifications:**

{% if panel.size %}
- Size: {{ panel.size }}
{% endif %}
{% if panel.resolution %}
- Resolution: {{ panel.resolution }}
{% endif %}
{% if panel.interface %}
- Interface: {{ panel.interface }}
{% endif %}
{% if panel.brightness %}
- Brightness: {{ panel.brightness }}
{% endif %}
{% if panel.temperature %}
- Operating temperature: {{ panel.temperature }}
{% endif %}
{% endif %}

{% if panel.tags %}
**Tags:**
{% for tag in panel.tags %}
`{{ tag }}`
{% endfor %}
{% endif %}

---

{% endunless %}
{% endunless %}
{% endfor %}

## Common TFT Display Interfaces

TFT LCD modules used in embedded SBC projects may use different display interfaces depending on resolution, system architecture, cable length, and product requirements.

### LVDS

LVDS is widely used in industrial display systems. It provides stable signal transmission for medium and large TFT LCD panels and is commonly used with 7-inch, 10.1-inch, 12.1-inch, and 15.6-inch display modules.

LVDS is often suitable for industrial HMI panels, control terminals, medical equipment, EV charger displays, and machine interface products.

### MIPI DSI

MIPI DSI is common in compact embedded systems, Android panels, smart home control panels, and mobile-style display products. It supports high-speed serial display transmission with fewer signal lines than RGB.

MIPI DSI integration usually requires correct panel initialization commands, lane configuration, timing parameters, reset sequence, and backlight control.

### RGB

RGB display interfaces are common in lower-resolution embedded panels. RGB is straightforward and widely supported by many ARM SoCs, but it requires more signal lines than LVDS or MIPI DSI.

RGB panels are often used in cost-sensitive HMI products, small industrial displays, and simple control terminals.

### eDP

eDP is often used for higher-resolution panels, especially notebook-style display modules such as 13.3-inch, 15.6-inch, or larger Full HD panels. It is suitable for products that need higher resolution and cleaner internal cabling.

## Typical Display Bring-Up Checklist

When integrating a TFT LCD with an embedded SBC, engineers should verify both hardware and software configuration.

1. Confirm the LCD panel datasheet.
2. Check display interface type and pin mapping.
3. Verify panel power rails.
4. Confirm reset GPIO and enable GPIO.
5. Configure backlight PWM and enable pin.
6. Check panel timing parameters.
7. Confirm Device Tree panel node.
8. Verify LCD connector wiring.
9. Test display output during boot.
10. Confirm touch panel interface and interrupt pin.
11. Check screen rotation and coordinate mapping.
12. Test brightness adjustment.
13. Validate display stability under long-time operation.
14. Test the final enclosure for EMI, grounding, and thermal behavior.

## Related Technical Posts

- [How to Debug Linux LCD Backlight Problems on Embedded SBCs](/posts/how-to-debug-linux-lcd-backlight/)
- [GitHub Display Config](/github-display-config)
- [RK050BHD335 PX30 Android Setup](/rk050bhd335-px30-android-setup)

## Related SBC Guides

- [SBC Guides](/sbc/)
- [Get IP of SBC](/get-ip-of-SBC)
- [Setup ADB on Windows](/setup-adb-on-windows)
- [Upgrade Android OTA via ADB](/upgrade-android-ota-via-adb)

## GitHub Repository

The display configuration examples are also maintained in the GitHub repository:

[rocktech-tft-display-configs](https://github.com/Kevin109/rocktech-tft-display-configs)

This repository includes example Device Tree configuration files, display notes, and panel integration references for Rockchip-based embedded SBC projects.

## Notes for Developers

The files in this section are intended as practical references. Actual display configuration may vary depending on the SBC model, SoC version, kernel version, Android or Linux BSP, panel revision, touch controller, and board-level wiring.

Before using a configuration in production, always compare it with:

- The LCD panel datasheet
- The SBC schematic
- The board connector pinout
- The SoC display controller documentation
- The Linux or Android BSP source code
- The actual display cable and touch panel configuration

A working display configuration depends on both hardware design and software setup. Device Tree files should be treated as board-specific engineering references, not universal drop-in configurations.