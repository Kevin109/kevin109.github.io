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

{% if post.tags %}
**Tags:** 
{% for tag in post.tags %}
`{{ tag }}`
{% endfor %}
{% endif %}

---
{% endunless %}
{% endunless %}
{% endunless %}
{% endfor %}

## Recommended Reading Path

If you are new to TFT display configuration on embedded SBCs, start with the backlight and Device Tree related articles first, then move to specific Rockchip display examples.

Suggested order:

1. Linux LCD backlight debugging
2. Device Tree panel node basics
3. LVDS, MIPI DSI, RGB, and eDP interface selection
4. Rockchip display configuration examples
5. Specific TFT module setup guides

## Related Sections

- [TFT Config Index](/tft-config/)
- [SBC Guides](/sbc/)
- [GitHub Display Config](/github-display-config/)
- [RK050BHD335 PX30 Android Setup](/rk050bhd335-px30-android-setup/)