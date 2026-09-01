<p align="center">
  <img src="https://raw.githubusercontent.com/sjauijn/adguard-home-plus-HAOS/main/adguard/icon.png" alt="icon">
</p>

# AdGuard Home Plus — Home Assistant App

I maintain this app, along my other apps and custom integrations for the Home Assistant, solely for my own use. As long as I'm actively using them myself, I'll continue developing and updating them; otherwise, support for apps and(or) custom integrations I no longer need will be discontinued.

## Configuration

**Note**: _Remember to restart the app when the configuration is changed._

Example app configuration:

```yaml
log_level: info
ssl: true
certfile: fullchain.pem
keyfile: privkey.pem
```

**Note**: _This is just an example, don't copy and paste it! Create your own!_

### AdGuardHome.yaml location

The main AdGuard Home configuration file is stored at:

```
/addon_configs/adguard/AdGuardHome.yaml
```

This path is accessible via SFTP (e.g. using WinSCP, Cyberduck, or the
VS Code Remote SSH extension) without needing Portainer or Docker console
access. Runtime data (query log, statistics, filter databases) remains in
`/data/adguard/` as in the original app.

### Option: `log_level`

The `log_level` option controls the level of log output by the app and can
be changed to be more or less verbose, which might be useful when you are
dealing with an unknown issue. Possible values are:

- `trace`: Show every detail, like all called internal functions.
- `debug`: Shows detailed debug information.
- `info`: Normal (usually) interesting events.
- `notice`: Normal but significant events.
- `warning`: Exceptional occurrences that are not errors.
- `error`: Runtime errors that do not require immediate action.
- `fatal`: Something went terribly wrong. App becomes unusable.

Please note that each level automatically includes log messages from a
more severe level, e.g., `debug` also shows `info` messages. By default,
the `log_level` is set to `info`, which is the recommended setting unless
you are troubleshooting.

### Option: `ssl`

Enables/Disables SSL (HTTPS) on the app. Set it `true` to enable it,
`false` otherwise.

**Note**: _The SSL settings only apply to direct access and has no effect
on the Ingress service._

### Option: `certfile`

The certificate file to use for SSL.

**Note**: _The file MUST be stored in `/ssl/`, which is the default_

### Option: `keyfile`

The private key file to use for SSL.

**Note**: _The file MUST be stored in `/ssl/`, which is the default_

### Option: `leave_front_door_open`

Adding this option to the app configuration allows you to disable
authentication on the AdGuard Home by setting it to `true`.

**Note**: _We STRONGLY suggest, not to use this, even if this app is
only exposed to your internal network. USE AT YOUR OWN RISK!_

## Encryption Settings (Advanced Usage)

AdGuard Home allows the configuration of running DNS-over-HTTPS and
DNS-over-TLS locally. If you configure these options please ensure to restart
the app afterwards. Also to use DNS-over-HTTPS correctly please ensure to
configure SSL on the app as well as in AdGuard Home itself. Also consider
that the app and AdGuard Home cannot use the same port for SSL.

## Accessing the AdGuard Home API (Advanced Usage)

AdGuard Home ships an HTTP API, served under `/control`, which you can use to
query the app remotely, for example to analyze the query log from somewhere
else.

Ingress is not usable for this. It is built around a Home Assistant session
and rewrites the paths it proxies, so it is not something an external API
client can talk to. Use the direct web interface port instead, which is
disabled by default: set a port for `80/tcp` in the Network section of the app
configuration and restart the app. The API is then available on that port,
for example `http://<your-instance>:<port>/control/status`.

Take note of the authentication, because two layers are involved and they can
collide. NGINX sits in front of AdGuard Home and, by default, checks every
request to the direct port against Home Assistant using HTTP basic auth. That
same `Authorization` header is passed on to AdGuard Home, whose API also uses
basic auth. If you have users configured inside AdGuard Home, it does not
recognize your Home Assistant credentials and answers `401`, even though the
request made it past NGINX.

Two combinations work:

- Keep the Home Assistant check enabled and configure no users inside AdGuard
  Home. Your Home Assistant credentials get you through NGINX, and AdGuard
  Home does not ask for anything.
- Set `leave_front_door_open` to `true` and configure users inside AdGuard
  Home. NGINX stops checking, AdGuard Home's own basic auth applies, and your
  API client authenticates against AdGuard Home directly.

**Note**: _The warning on `leave_front_door_open` above is aimed at enabling
it while AdGuard Home itself has no users configured, which leaves the app
completely unauthenticated. Only expose this port on your local network._
