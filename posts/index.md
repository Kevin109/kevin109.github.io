---
layout: custom
title: "Technical Posts"
description: "Technical articles about Rockchip SBC display configuration, Linux LCD backlight debugging, Device Tree panel nodes, TFT LCD integration, and embedded SBC development."
permalink: /posts/
---

# Technical Posts

This section collects practical engineering notes and tutorials for embedded SBC display integration, Rockchip Linux/Android development, TFT LCD configuration, Device Tree setup, backlight debugging, and related hardware bring-up topics.

## Latest Posts

{% assign post_pages = site.pages | where_exp: "page", "page.path contains 'posts/'" | sort: "date" | reverse %}

{% for post in post_pages %}
{% unless post.path contains '_index.md' %}
{% unless post.path contains 'index.md' %}
{% unless post.title == nil %}
### [{{ post.title }}]({{ post.url | relative_url }})

{% if post.date %}
**Date:** {{ post.date | date: "%Y-%m-%d" }}
{% endif %}

{% if post.description %}
{{ post.description }}
{% endif %}

<!-- {% if post.tags %}
**Tags:** 
{% for tag in post.tags %}
`{{ tag }}`
{% endfor %}
{% endif %} -->

{% if post.tags %}
<div class="post-tags">
  <span class="post-tags-label">Tags:</span>
  {% for tag in post.tags %}
    <span class="post-tag">{{ tag }}</span>
  {% endfor %}
</div>
{% endif %}

---
{% endunless %}
{% endunless %}
{% endunless %}
{% endfor %}

## Recommended Reading Path

If you are new to TFT display configuration on embedded SBCs, start with the backlight and Device Tree related articles first, then move to specific Rockchip display examples.

Suggested order:

1. [MIPI vs LVDS vs RGB display interface](/posts/mipi-vs-lvds-vs-rgb-display-interface/)
2. [How to choose a TFT LCD for embedded Linux](/posts/how-to-choose-tft-lcd-for-embedded-linux/)
3. [Linux LCD backlight debugging](/posts/how-to-debug-linux-lcd-backlight/)
4. Device Tree panel node basics
5. Rockchip display configuration examples
6. Specific TFT module setup guides

## Selection Guides

- [5 Inch vs 7 Inch TFT Display for HMI Products](/posts/5-inch-vs-7-inch-tft-display-for-hmi/)
- [Android SBC vs Linux SBC for Industrial Display Products](/posts/android-sbc-vs-linux-sbc-for-industrial-display/)
- [RK3566 vs RK3568 for Embedded HMI Products](/posts/rk3566-vs-rk3568-for-embedded-hmi/)

## Related Sections

- [TFT Config Index](/tft-config/)
- [SBC Guides](/sbc/)
- [GitHub Display Config](/github-display-config)
- [RK050BHD335 PX30 Android Setup](/rk050bhd335-px30-android-setup)
