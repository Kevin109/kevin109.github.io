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

## Rotation Strategy

There are two common strategies. The first is to keep the system framebuffer in the panel's native orientation and force the application to render in the desired orientation. This can be enough for a single-purpose kiosk app, but boot animation, system dialogs, and recovery screens may still appear in the wrong direction.

The second strategy is to configure the system orientation so Android treats the panel as the final product orientation. This is usually better for commercial devices, but it requires proper touch mapping and framework configuration.

Choose the strategy before tuning the application. If the hardware is portrait but the product is landscape, document which layer owns the rotation.

## Boot Logo and Boot Animation

Users notice rotation problems during boot. A correct app orientation does not help if the boot logo is sideways. Rockchip Android products may have separate handling for loader logo, kernel logo, boot animation, Android launcher, and the final app.

Check each stage:

1. Loader or U-Boot logo
2. Kernel boot logo if enabled
3. Android boot animation
4. Launcher
5. Main application
6. Recovery or OTA screen

The files and settings vary by BSP version, so verify on the actual firmware branch used for production.

## Touch and UI Density

After rotation, touch coordinates must match visual coordinates. Test all four corners, edge gestures if used, and multi-touch if the product requires it. If X and Y are swapped or one axis is inverted, users will immediately notice.

Also check Android density and layout. A portrait panel rotated to landscape may have a different expected density than the default BSP. Buttons can become too small or text may be clipped if density and resolution are not tuned.

## App-Level Orientation

For a dedicated product app, set orientation intentionally. Do not rely on accidental auto-rotation. In many embedded products, the accelerometer is absent, disabled, or irrelevant. The product should boot into the correct orientation every time.

If using WebView or a browser-based UI, test CSS viewport behavior after rotation. Some issues are not display driver bugs; they are layout assumptions in the application.

## Factory and Field Testing

Rotation should be part of production test. A simple touch test screen with corner targets can catch wrong touch orientation before shipment. For field updates, test whether OTA or recovery screens remain usable after rotation settings are changed.

## Common Rotation Mistakes

Common mistakes include fixing rotation only inside the app, forgetting recovery mode, leaving the boot animation sideways, or correcting the display while touch remains inverted. Another frequent issue is using a panel in portrait orientation but designing the UI as if it were native landscape, which can create density and layout problems.

For products with external HDMI and internal LCD, confirm whether rotation should apply to both outputs or only the internal display. A setting that fixes the built-in panel may make an external monitor wrong.

## Handoff Notes for App Developers

Hardware and BSP engineers should tell app developers the final logical resolution, density, orientation, and whether the system supports rotation changes at runtime. This avoids UI layouts that only work on the development monitor but fail on the production panel.

## Related Guides

- [Rockchip Android SBC Development Guide](/sbc/rockchip-android-sbc-development/)
- [RK050BHD335 PX30 Android Setup](/rk050bhd335-px30-android-setup)
- [TFT Config Index](/tft-config/)
