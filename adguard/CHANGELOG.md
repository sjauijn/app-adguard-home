## v6.2.1-plus (v0.107.79)
- Added Russian Translate for Configuration page (added ru.yaml)
- Updated to the latest AdGuard Home release - 0.107.79
- Updated base image to ghcr.io/hassio-addons/base:21.0.3
- Updated bundled NGINX to 1.30.4-r1
- App now waits up to 5 minutes for the host network to become available on
  startup, so DNS bind hosts are collected correctly after a reboot instead
  of only binding to localhost
- Fixed schema-migration warning that previously failed to log due to a
  non-existent `bashio::warning` call
- Simplified the 169.254.0.0/16 (link-local) address check
- Tightened NGINX response headers (dropped the deprecated
  `X-XSS-Protection` header, added `always` to security headers so they are
  sent on error responses too)
- Added Hebrew translation for the app configuration
- Documented how to reach the AdGuard Home HTTP API directly (bypassing
  Ingress) and how its authentication interacts with the app's own
  Home Assistant login check

## v6.2.0-plus (v0.107.77)
- Updated to the latest AdGuard Home release - 0.107.77

## v6.1.3-plus (v0.107.74)
- Make AdGuard Home on Home Assistant **Perfect! ^_^**
<p>
  <img src="https://raw.githubusercontent.com/sjauijn/adguard-home-plus-HAOS/main/images/perfect.jpg" alt="icon">
</p>
