---
title: "Device Tree Panel Timing Explanation"
description: "Explanation of TFT LCD panel timing fields in Linux Device Tree, including pixel clock, active area, sync width, front porch, back porch, polarity, and common configuration mistakes."
date: 2026-07-03
category: display-configuration
tags: [Device Tree, Panel Timing, TFT LCD, LVDS, MIPI DSI, RGB, Embedded Linux]
---

# Device Tree Panel Timing Explanation

Panel timing tells the display controller how to generate image data for a TFT LCD. In Linux Device Tree, timing values usually describe the active resolution, blanking intervals, sync signals, pixel clock, and signal polarity.

Wrong timing can cause no image, flicker, shifted image, wrong refresh rate, or unstable display output.

## Core Timing Fields

Common timing fields include:

- `clock-frequency`: pixel clock in Hz
- `hactive`: active horizontal pixels
- `vactive`: active vertical lines
- `hfront-porch`: pixels after active data before HSYNC
- `hback-porch`: pixels after HSYNC before active data
- `hsync-len`: HSYNC pulse width
- `vfront-porch`: lines after active data before VSYNC
- `vback-porch`: lines after VSYNC before active data
- `vsync-len`: VSYNC pulse width
- `hsync-active`: HSYNC polarity
- `vsync-active`: VSYNC polarity
- `de-active`: data enable polarity
- `pixelclk-active`: pixel clock sampling edge

The active area is the visible resolution. The porch and sync values are not visible, but they are required for correct scan timing.

## Pixel Clock

Pixel clock is based on total pixels per frame and refresh rate:

```text
pixel clock = htotal x vtotal x refresh rate
```

Where:

```text
htotal = hactive + hfront-porch + hsync-len + hback-porch
vtotal = vactive + vfront-porch + vsync-len + vback-porch
```

Use the panel datasheet as the reference. Do not calculate a new timing unless the panel supports a range.

## Common Mistakes

- Using only resolution and ignoring porch values
- Copying timing from a different panel size
- Wrong pixel clock unit
- Wrong HSYNC or VSYNC polarity
- Wrong DE polarity for RGB or LVDS panels
- Forgetting dual-channel LVDS bandwidth
- Changing refresh rate without checking panel limits

## Related Guides

- [How to Debug LVDS Display on RK3568](/tft-config/how-to-debug-lvds-display-on-rk3568/)
- [LCD Backlight Turns On but No Image](/tft-config/lcd-backlight-turns-on-but-no-image/)
- [TFT Config Index](/tft-config/)
