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

## Reading a Datasheet Timing Table

Most LCD datasheets provide a timing table with typical, minimum, and maximum values. The typical values are the safest starting point. Minimum and maximum values are allowed ranges, not recommended values for every design.

For each field, map the datasheet name to the Device Tree field. Datasheets may use names such as HFP, HBP, HPW, VFP, VBP, VPW, DCLK, PCLK, or DOTCLK. The names vary by vendor, but the meaning is consistent: active pixels plus blanking intervals produce a full frame.

If the datasheet provides a total horizontal period and active horizontal pixels, the remaining values are distributed across front porch, sync width, and back porch. Do not guess this distribution if the table provides exact numbers.

## Example Review Process

When adding a new panel, create a simple timing review note:

```text
Resolution: 1024 x 600
Pixel clock: from datasheet typical value
Horizontal: active + front porch + sync + back porch
Vertical: active + front porch + sync + back porch
Refresh: confirm calculated result is close to expected value
Polarity: match datasheet
```

This makes it easier to catch mistakes before booting the board. A single swapped porch value may still produce a mode, but the panel may not lock correctly.

## Timing and Interface Type

RGB panels depend heavily on DE, sync, and pixel clock edge because the display bus directly carries parallel pixel data.

LVDS panels also need correct timing, but additional details such as VESA or JEIDA mapping and channel count matter.

MIPI DSI video mode uses timing too, but MIPI panels may also need initialization commands. A correct timing table alone is not enough if the panel remains in sleep mode.

## Debugging Timing Problems

Timing problems often look like:

- Shifted image
- Rolling image
- Flickering image
- No image with backlight on
- Wrong refresh rate
- Image appears only at some temperatures

When debugging, change only one timing group at a time. If the panel vendor provides a working Linux or Android example, compare the numbers exactly. If the SoC clock framework rounds the pixel clock, check the actual clock reported in logs.

## Production Considerations

For production, timing should be validated across multiple panel samples and temperature conditions. Some panels tolerate loose timing on the bench but fail after long operation or at low temperature. Keep the final timing values documented with the panel part number and revision.

## Relationship With Backlight and Touch

Panel timing only controls how pixel data is sent to the LCD. It does not enable the LED backlight and it does not configure the touch panel. This matters because engineers sometimes change timing values while the real issue is a disabled backlight or wrong touch orientation.

Bring up the display in layers. First confirm power and reset. Then confirm panel timing and image output. Then enable backlight brightness control. Finally add touch input and rotation. This order makes failures easier to isolate.

## Version Control Advice

When working with multiple panels, avoid editing one shared timing node without recording which product uses it. Give each panel a clear compatible string or configuration file. A later copy-paste change for one LCD should not silently change another product.

## Related Guides

- [How to Debug LVDS Display on RK3568](/tft-config/how-to-debug-lvds-display-on-rk3568/)
- [LCD Backlight Turns On but No Image](/tft-config/lcd-backlight-turns-on-but-no-image/)
- [TFT Config Index](/tft-config/)
