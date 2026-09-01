<p align="center">
  <img src="https://raw.githubusercontent.com/sjauijn/adguard-home-plus-HAOS/main/adguard/icon.png" alt="icon">
</p>

# AdGuard Home Plus

I maintain this app, along with my other Home Assistant apps, solely for my own use. As long as I'm actively using them myself, I'll continue developing and updating them; otherwise, support for apps I no longer need will be discontinued.

## What's different from the original app

This fork moves `AdGuardHome.yaml` from the internal `/data/adguard/` directory
to `/addon_configs/adguard/`, making it accessible via SFTP without needing
Portainer or Docker console access.

| | Original | This fork |
|---|---|---|
| `AdGuardHome.yaml` location | `/data/adguard/` | `/addon_configs/adguard/` |
| Accessible via SFTP | ❌ | ✅ |
| Query log, stats, filters DB | `/data/adguard/` | `/data/adguard/` (unchanged) |

## About

AdGuard Home is a network-wide ad-and-tracker blocking DNS server with
parental control (adult content blocking) capabilities. Its purpose is to let
you control your entire network and all your devices, and it does not require
using a client-side program.

AdGuard Home provides a beautiful, easy and feature-rich web interface to
easily manage the filtering process and its settings.

<p>
  <img src="https://raw.githubusercontent.com/sjauijn/adguard-home-plus-HAOS/main/images/screenshot.jpg" alt="icon">
</p>

## Installation

1. **Ensure your Home Assistant device has a
   [static IP and static external DNS servers!](https://developers.home-assistant.io/docs/operating-system/network)**
   This is important! You **WILL** end up having issues if you skip this step.
   - Change this setting in Network:
     [![Open your Home Assistant instance and manage your systems network configuration.](https://my.home-assistant.io/badges/network.svg)](https://my.home-assistant.io/redirect/network/)
     (_Settings → System → Network
     → Configure network interfaces → Your Interface → IPv4 → Static_)
   - Please note, setting a fixed IP in your router is **NOT** static.

2. Click to add the stable repository:
   [![Add Stable Repository](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https://github.com/sjauijn/adguard-home-plus-HAOS)

   Or manually add:

   ```text
   https://github.com/sjauijn/adguard-home-plus-HAOS
   ```
