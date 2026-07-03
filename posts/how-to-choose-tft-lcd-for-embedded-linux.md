---
layout: custom
title: "How to Choose a TFT LCD for Embedded Linux Projects"
description: "A practical guide to choosing a TFT LCD for embedded Linux products, covering size, resolution, interface, touch, backlight, Device Tree support, and long-term supply."
date: 2026-07-03
category: display-selection
tags: [TFT LCD, Embedded Linux, Device Tree, LVDS, MIPI DSI, RGB, HMI]
---

# How to Choose a TFT LCD for Embedded Linux Projects

Choosing a TFT LCD for an embedded Linux product is not only a screen-size decision. The display affects the PCB design, enclosure, power budget, kernel configuration, Device Tree, backlight circuit, touch panel integration, EMI behavior, production testing, and long-term maintenance.

A good display choice is one that the hardware, software, and mechanical design can support reliably. A poor choice may look attractive in a datasheet but create weeks of bring-up work.

## Start With the Product Use Case

Before comparing panel specifications, define what the product needs to do.

Important questions include:

- Is the screen the main user interface?
- Will the product run a simple UI or a complex graphical application?
- Is the product used indoors, outdoors, or in a factory?
- Does the user operate it with gloves?
- Does it need wide temperature support?
- Is long-term supply more important than the lowest price?
- Does the enclosure limit display thickness or cable direction?

For an industrial HMI, reliability and supply stability may matter more than very high resolution. For a smart control panel, appearance, touch response, brightness, and viewing angle may be more important.

## Check the SBC Display Output First

The selected LCD must match the display outputs available on the SBC or SoC. Common interfaces include MIPI DSI, LVDS, RGB, HDMI, and eDP.

If the board only exposes LVDS, choosing a MIPI panel adds bridge IC cost and complexity. If the board exposes MIPI DSI but the panel requires RGB, the design may need a different panel, a different board, or a conversion chip.

For interface tradeoffs, see [MIPI vs LVDS vs RGB Display Interface](/posts/mipi-vs-lvds-vs-rgb-display-interface/).

## Match Resolution to Performance

Higher resolution is not always better in embedded Linux. It increases memory bandwidth, GPU or display controller workload, boot logo size, UI rendering cost, and sometimes power consumption.

Common practical choices:

- 480x272 or 800x480 for simple control panels
- 1024x600 for 7-inch HMI products
- 1280x800 for 10.1-inch industrial panels
- 1920x1080 for products that need detailed visuals

Before selecting a high-resolution panel, confirm that the SoC display controller, memory bandwidth, graphics stack, and application UI can handle it smoothly.

## Confirm Device Tree and Driver Support

Embedded Linux display bring-up usually depends on Device Tree. The LCD panel may need panel timing, power rails, reset GPIO, enable GPIO, backlight configuration, and sometimes initialization commands.

Ask for these items before committing to a display:

- Panel datasheet
- Timing table
- Power sequence
- Connector pin definition
- Backlight voltage and current
- Touch controller model
- Example Device Tree if available
- Linux kernel version used in reference projects

If the panel vendor or SBC vendor can provide a known working Device Tree example, the project risk is lower.

## Do Not Treat Backlight as an Afterthought

Many display failures are actually backlight failures. The LCD may be receiving image data correctly, but the user sees a black screen because the LED backlight is not enabled.

Check:

- Backlight input voltage
- LED current requirement
- Whether the panel needs a separate LED driver
- PWM dimming pin
- Enable pin polarity
- Brightness range
- Thermal behavior at full brightness

For debugging details, see [How to Debug Linux LCD Backlight Problems on Embedded SBCs](/posts/how-to-debug-linux-lcd-backlight/).

## Touch Panel Selection

If the display uses capacitive touch, confirm the touch controller before ordering. Most embedded Linux touch panels use I2C plus interrupt and reset pins.

Important checks:

- Touch controller model
- Kernel driver availability
- I2C address
- Interrupt GPIO
- Reset GPIO
- Coordinate rotation
- Cover glass thickness
- Glove or wet-touch requirement

Display rotation and touch coordinate rotation must be planned together. Otherwise the image may rotate correctly while touch input remains wrong.

## Supply and Production Considerations

For commercial products, do not choose a display only because a sample is available. Confirm long-term supply, panel revision control, connector stability, and acceptable alternatives.

A practical display choice should include:

- Stable availability
- Clear revision policy
- Replacement model plan
- Mechanical drawing
- Optical specifications
- Electrical specification
- Test procedure
- Vendor support during bring-up

## Practical Selection Checklist

1. Confirm product screen size and viewing distance.
2. Confirm SBC display output.
3. Choose the interface: MIPI DSI, LVDS, RGB, HDMI, or eDP.
4. Select a resolution that the SoC can handle.
5. Verify panel timing and power sequence.
6. Check backlight voltage, current, PWM, and enable pin.
7. Confirm touch controller support.
8. Review connector pinout and cable direction.
9. Validate Device Tree support.
10. Test display, touch, brightness, suspend/resume, and long-time operation.

## Related Guides

- [5 Inch vs 7 Inch TFT Display for HMI](/posts/5-inch-vs-7-inch-tft-display-for-hmi/)
- [RK3568 LVDS Display Configuration Guide](/posts/rk3568-lvds-display-configuration/)
- [TFT Config Index](/tft-config/)
- [GitHub Display Config](/github-display-config)
