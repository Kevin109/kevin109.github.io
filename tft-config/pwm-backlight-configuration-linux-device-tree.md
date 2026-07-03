---
title: "PWM Backlight Configuration in Linux Device Tree"
description: "Practical guide to configuring PWM backlight in Linux Device Tree for TFT LCD panels, including PWM channel, enable GPIO, brightness levels, polarity, and debugging steps."
date: 2026-07-03
category: display-configuration
tags: [PWM Backlight, Linux Device Tree, TFT LCD, Backlight, GPIO, Embedded Linux]
---

# PWM Backlight Configuration in Linux Device Tree

Most embedded TFT LCD products use a separate LED backlight circuit. Linux usually controls brightness through a `pwm-backlight` node in Device Tree. If this node is wrong, the panel may show no visible image even when the display data path is working.

## Typical Backlight Node

A simplified Device Tree example looks like this:

```dts
backlight: backlight {
    compatible = "pwm-backlight";
    pwms = <&pwm0 0 25000 0>;
    brightness-levels = <0 32 64 128 192 255>;
    default-brightness-level = <5>;
    enable-gpios = <&gpio1 3 GPIO_ACTIVE_HIGH>;
};
```

Actual syntax depends on the kernel, SoC, and board pin naming.

## What Each Field Means

- `compatible`: selects the PWM backlight driver
- `pwms`: selects PWM controller, channel, period, and polarity
- `brightness-levels`: maps brightness index to PWM duty value
- `default-brightness-level`: default index at boot
- `enable-gpios`: optional GPIO that enables the backlight driver

The PWM controls brightness. The enable GPIO often turns the LED driver on or off.

## Debug Checklist

Check:

- PWM controller is enabled
- PWM pinctrl is configured
- PWM channel matches schematic
- PWM period is suitable for the LED driver
- Enable GPIO polarity is correct
- Backlight power input is present
- Panel node references the backlight node if required

If brightness control appears in Linux but the screen stays dark, measure the PWM pin and backlight enable pin.

## Related Guides

- [How to Debug Linux LCD Backlight Problems on Embedded SBCs](/posts/how-to-debug-linux-lcd-backlight/)
- [LCD Backlight Turns On but No Image](/tft-config/lcd-backlight-turns-on-but-no-image/)
- [Device Tree Panel Timing Explanation](/tft-config/device-tree-panel-timing-explanation/)
