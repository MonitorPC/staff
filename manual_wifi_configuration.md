# Manual Wi-Fi configuration (no NetworkManager)

**Tested on**: Debian 13(Live USB)
**Objective**: Configure a wireless interface without using NetworkManager, using the persistent Debian tools

## Prerequisites

- Live USB: [debian-live-13.6.0-amd64-standard.iso](https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/debian-live-13.6.0-amd64-standard.iso)

## Description

There are serveral approaches to configure wireless device to connect Wi-Fi. But when we limited by environment like Live USB, the number of available tools decrease sharply.
On Debian 13 we have to work with tools like `ifupdown`, `wpa_supplicant` and `dhcpcd`. And dont forget about `ip` command.

One of the ways to configure Wi-Fi is `ifupdown` package with `wpa_supplicant` tools.
- First we need find out our wireless network device.
To do that we can type `ip a`. `Wlan*` or `wlp*s*` will be one we are looking for.

- Now we need to configure `ifupdown interfaces`.
Open the `/etc/network/interfaces` and type next:
```
  auto wlp*s*
  iface wlp*s* inet dhcp
      wpa-conf /tmp/ws.conf
```
It will say `ifup` command to start `wlp*s*` interface and use `wpa_supplicant` tools.

- But before we need to say which network we want to connect and its password.
It can easly done by `wpa_passphrase "Your Wi-Fi SSID" "Your Wi-Fi pw" > /tmp/ws.conf`.
As you can mentioned we use same `/tmp/ws.conf` as in `/etc/network/interface`.

- Now we ready to connect.
Run `ifup wlp*s*`. This command will connect the your AP by using `wpa_supplicant`, then recive the IP by `dhcpcd`.

- Test your connection.
`ping google.com`

- Troubleshouting.
TO DO

