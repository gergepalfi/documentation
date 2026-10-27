## Overview

The OpenWrt Project is a Linux operating system targeting embedded devices, which is often used as an open-source solution for routers and firewalls.

This guide covers setting Quad9 as upstream DNS for OpenWrt, this means all traffic, including the router itself, will use Quad9 instead of your ISP's DNS.

!!! warning "Backup Time!"
    Before making changes to a production environment, we recommend [backing up the existing configuration](https://openwrt.org/docs/guide-user/troubleshooting/backup_restore)

## Instructions

* Log into your LuCI control panel, typically by opening `http://192.168.1.1` in your browser.

* Navigate to `Network` -> `Interfaces`
    * Edit `wan` interface
    * Select `Advanced Settings` tab
    * uncheck `Use DNS servers advertised by peer`
    * add `9.9.9.9` and `149.112.112.112` to `Use custom DNS servers` list that appears.
    * `Save` then `Save & Apply`

* Repeat the same steps above for the `wan6` interface to add `2620:fe::fe` and `2620:fe::9`, or the IPv6 addresses of your preferred Quad9 service.

When complete, you should see the Quad9 IPs listed on the Overview page under your Upstream connections for DNS

[Source](https://forum.openwrt.org/t/right-way-to-change-the-dns/220983/2) from OpenWrt forum

## Alternative Approaches

There are multiple other ways to set DNS in OpenWrt for other cases, for these please do your own research:
* `Network > Interfaces > lan > DHCP Server > General Setup > DHCP-Options`
    * advertises quad9 DNS to clients that connect to lan interface
* `Network > DNS > Forwards > DNS Forwards`
    * Forward specific domain queries to specific upstream servers.

## Verify Configuration

* Confirm you're using Quad9 on Linux, MacOS, or Windows using [on.quad9.net](https://on.quad9.net/).

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
