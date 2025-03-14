# Home Assistant UV Index Card

HAOS UV Index Card is a professional Lovelace UI card for Home Assistant that displays the real-time UV Index based on data from sensor.outdoor_uv_index. The card provides color-coded risk levels and protection recommendations according to WHO guidelines. It uses Mushroom Cards for a modern and clean design, making it easy to assess UV exposure at a glance.

This project is designed for Home Assistant OS (HAOS) and requires HACS for installation. The card is ideal for anyone who wants to monitor UV radiation and take appropriate sun protection measures directly from their Home Assistant dashboard.

## Features

- Displays real-time **UV Index** from `sensor.outdoor_uv_index`  
- **Color-coded risk level** (Green, Yellow, Orange, Red, Purple)  
- Shows **WHO protection recommendations** 
- **Simple and professional** Lovelace design  

## Requirements

- **Home Assistant OS (HAOS)**  
- **HACS installed**  
- **Mushroom Cards** (via HACS → Frontend → "Mushroom Cards")  

## Installation

1. Install **Mushroom Cards** in HACS  
2. Add the following Lovelace YAML to your **Dashboard**  

## Lovelace YAML

```yaml
type: custom:mushroom-template-card
primary: "UV Index: {{ states('sensor.outdoor_uv_index') }}"
secondary: >
  {% set uv = states('sensor.outdoor_uv_index') | float(0) %}
  {% if uv < 3 %} 🟢 Low - No protection needed
  {% elif uv < 6 %} 🟡 Moderate - Stay in shade, use SPF 30
  {% elif uv < 8 %} 🟠 High - SPF 30+, wear a hat and sunglasses
  {% elif uv < 11 %} 🔴 Very High - SPF 50+, protective clothing
  {% else %} 🟣 Extreme - Avoid sun exposure, SPF 50+
  {% endif %}
icon: mdi:white-balance-sunny
icon_color: >
  {% set uv = states('sensor.outdoor_uv_index') | float(0) %}
  {% if uv < 3 %} green
  {% elif uv < 6 %} yellow
  {% elif uv < 8 %} orange
  {% elif uv < 11 %} red
  {% else %} purple
  {% endif %}
layout: vertical
multiline_secondary: true
fill_container: true
```
