---
title: "How I Drove the RK050BHD335 TFT Display Using PX30 SBC with a Custom Adapter Board"
seo_title: "How I Drove the RK050BHD335 TFT Display Using PX30 SBC with a Custom Adapter Board"
description: "A step-by-step guide to integrating the RK050BHD335 5-inch MIPI TFT display with the Rockchip PX30 SBC using a custom fly-wire adapter. Includes device tree tweaks, panel timing, and driver configuration under Android 11."
date: 2025-06-29
keywords: ["RK-Android-PX30-01", "5-inch TFT", "Android SBC", "Custom board", "TFT display"]
---

# How I Drove the RK050BHD335 TFT Display Using PX30 SBC with a Custom Adapter Board

Recently, I worked on a small integration project using the [Rocktech RK-Android-PX30-01 SBC](https://www.rocktech.com.hk/rockchip-px30-sbc/) and a 5-inch TFT display — the RK050BHD335.

Since the interface and pinout of the display did not directly match the SBC, I designed a quick adapter board using fly wires to get everything up and running under Android.

![Hardware Setup](/rocktech-RK050BHD335-PX30.jpeg)

---

## Hardware Used

* **SBC:** Rocktech RK-Android-PX30-01
* **Display:** Rocktech RK050BHD335, 5-inch TFT, MIPI interface
* **Adapter:** Custom fly-wire board
* **OS:** Android 11 (vendor SDK)

---

## Why We Used a Fly-Wire Adapter

The RK-Android-PX30-01 and the RK050BHD335 screen differ in pin definition, voltage levels, and backlight current requirements. Designing a full custom SBC or even fabricating a new adapter board for a single test would take days or weeks.

Using a quick fly-wire adapter was the fastest way to validate the setup. It allowed us to:

* Remap signals manually
* Adjust power rails safely
* Validate display and backlight behavior without costly fabrication

This method is especially suitable in the prototyping phase when you're testing multiple display options before committing to a final design.

---

## Display Configuration and Device Tree Modifications

To drive the RK050BHD335, I needed to configure the device tree and panel parameters under the kernel and Android BSP.

🧹 Key settings included:

* Resolution: 720x1280
* MIPI DSI dual lane
* HS frequency tuning
* Panel timing adjustments
* Touch controller setup (if applicable)

### Device Tree Snippet

```dts
panel: panel {
  compatible = "rocktech,rk050bhd335";
  reg = <0>;
  backlight = <&backlight>;
  status = "okay";
};
```

You can find the full configuration files and source code on GitHub:
👉 [RK050BHD335 Display Config for PX30](/github-display-config)

---

## Challenges Faced

* **Panel reset timing mismatch:** Required tuning of delays in DTS.
* **Backlight GPIO control:** Needed manual GPIO selection and enable logic.
* **MIPI lane remapping:** Due to custom cable routing, lane polarity needed adjustment.
* **Voltage mismatch:** Ensured correct 1.8V/3.3V logic levels using resistors and fly-wire paths.

All issues were resolved through trial, datasheet review, and iterative kernel rebuilding.

---

## Result

After debugging and kernel rebuild, the RK050BHD335 panel powered on successfully with touch and Android UI running smoothly.

![Working Android Display](/rocktech-RK050BHD335-PX30.jpeg)

---

## Lessons Learned

* Always start with a known working screen for comparison.
* Use oscilloscope or logic analyzer to debug MIPI lane activity.
* Fly-wire boards are fragile but efficient for quick validation.

For production, a proper FPC-to-board adapter or integrated SBC design is necessary to ensure signal integrity and EMI compliance.

---

## References

* [Rocktech TFT Display Portfolio](https://www.rocktech.com.hk/industrial-tft-displays/)
* [PX30 Embedded Board Overview](https://www.rocktech.com.hk/rockchip-px30-sbc/)
* [GitHub Config Repo](https://github.com/Kevin109/rocktech-tft-display-configs/)

---

## Conclusion

This setup can be reused by others trying to integrate custom MIPI TFT panels with Rockchip PX30 or similar SoCs. If you're working with a different screen model, the same methodology applies: verify pin definitions, match power rails, adjust DTS and kernel sources, and validate with minimal hardware changes.

I plan to document more boards and panels in the coming weeks. Feel free to follow the [GitHub repo](/github-display-config) for updates and future configurations.
