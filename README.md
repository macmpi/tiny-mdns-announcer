[![latest packaged version(s)](https://repology.org/badge/latest-versions/tiny-mdns-announcer.svg)](https://repology.org/project/tiny-mdns-announcer/versions)

# Tiny mDNS Announcer
`tiny-mdns-ann` is a lightweight shell utility to announce device's `.local` hostname and network services via mDNS.\
Hostname can then be resolved by any machine supporting mDNS/Avahi LAN discovery.

`tiny-mdns-ann` only depends on `netcat`, as found in `busybox`, or other standalone implementations.\
It merely sends unsolicited UDP announcement packets, and does not answer queries.\
It is a best-effort lightweight announcer, and is not intended as a replacement for fully compliant mDNS responder.

## Features:
- hostname LAN IP address resolution
- optionally advertises `http` and `ssh` services
- IPv4 and IPv6 support
- OpenRC and Systemd services

## Benefits:
- extremely small footprint
- runs under POSIX shell on Linux, *BSD, macOS, Windows
- compatible with busybox's `nc`

## Setup procedure:
Make script executable and run `tiny-mdns-ann` on device as follows:
```
usage: tiny-mdns-ann [OPTIONS]

Announce HOSTNAME.local over mDNS on active interfaces.

Options:
  --help              Show this help.
  --host NAME         Host name to announce in the .local domain.
  --http[=PORT]       Advertise HTTP, default port 80.
  --ssh[=PORT]        Advertise SSH, default port 22.

Environment:
  INTERVAL            Announcement interval in seconds, default 60.
  ADVERTISE_IPV6      Enable IPv6 announcements, default 1.
  USE_SOURCE_ADDRESS  Use nc -s, default 1.
  DEBUG_LOG           Log each announcement, default 0.
```
Main execution steps are logged: `grep tiny-mdns-ann /var/log/messages`.

OpenRC and Systemd services files are provided to run `tiny-mdns-ann` as a boot service.\
A complete Alpine Linux [package](https://pkgs.alpinelinux.org/packages?name=tiny-mdns-announcer&branch=edge&repo=&arch=&origin=&flagged=&maintainer=) is also in the works.

[![Packaging status](https://repology.org/badge/vertical-allrepos/tiny-mdns-announcer.svg)](https://repology.org/project/tiny-mdns-announcer/versions)

*Note:*
- IPv6 link-local multicast requires interface scoping; this is handled automatically by the announcer.
- As `nc` does not allow multicast `ttl`/`hop-limit` controls, announcements do not set mDNS-required value of 255, but still work in most cases.
- If `socat` is available, it is used in place of `nc` to send announcements with `ttl`/`hop-limit` 255.

##
<a href='https://ko-fi.com/V7V81B2UF6' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://storage.ko-fi.com/cdn/kofi5.png?v=6' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>
