[![latest packaged version(s)](https://repology.org/badge/latest-versions/tiny-mdns-announcer.svg)](https://repology.org/project/tiny-mdns-announcer/versions)

# Tiny mDNS Announcer
`tiny-mdns-ann` is a lightweight shell utility to announce device's `.local` hostname and network services via mDNS.\
Hostname can then be resolved by any machine supporting mDNS/Avahi LAN discovery.

`tiny-mdns-ann` only depends on `netcat`, as found in `busybox`, or other standalone implementations.\
It merely sends unsolicited UDP announcement packets, and does not answer queries as a full mDNS responder would.

## Features:
- hostname LAN IP address resolution
- optionally advertises `http` and `ssh` services
- openRC and Systemd services

## Benefits:
- extremely small footprint
- run under POSIX shell
- compatible with busybox's bundled `netcat`

## Setup procedure:
Make script executable and run `tiny-mdns-ann` on device as follows:
```
usage: tiny-mdns-ann [--host <host-name>] [--http[=port]] [--ssh[=port]]

Simply annonces hostname.local IP address over mdns/avahi on LAN,
and optionally advertizes http (port 80) and/or ssh (port 22) services.
Only requires netcat from Busybox or standalone nc utility.
Lowest footprint & best-effort unsolicited announcer (not a mdns responder).

Options: --help              Help information and usage
         --host <host-name>  Specify host name to be announced in .local domain
         --http[=port]       Announce http service (port 80 by default)
         --ssh[=port]        Announce ssh service (port 22 by default)
```
Main execution steps are logged: `grep tiny-mdns-ann /var/log/messages`.

OpenRC and Systemd services files are provided to run `tiny-mdns-ann` as a boot service.\
A complete Alpine Linux [package](https://pkgs.alpinelinux.org/packages?name=tiny-mdns-announcer&branch=edge&repo=&arch=&origin=&flagged=&maintainer=) is also in the works.

[![Packaging status](https://repology.org/badge/vertical-allrepos/tiny-mdns-announcer.svg)](https://repology.org/project/tiny-mdns-announcer/versions)

##
<a href='https://ko-fi.com/V7V81B2UF6' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://storage.ko-fi.com/cdn/kofi5.png?v=6' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>
