# Manual Wi-Fi configuration (no NetworkManager)

**Tested on**: Debian 13 (Live USB)
**Objective**: Configure a wireless interface without using NetworkManager, using the persistent Debian tools

## Prerequisites

- Live USB: [debian-live-13.6.0-amd64-standard.iso](https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/debian-live-13.6.0-amd64-standard.iso)

## Description

There are several approaches to configure a wireless device to connect to Wi-Fi. But when we are limited by the environment like Live USB, the number of available tools decreases sharply.
On Debian 13 we have to work with tools like `ifupdown`, `wpa_supplicant` and `dhcpcd`. And don't forget about the `ip` command.

One of the ways to configure Wi-Fi is the `ifupdown` package with the `wpa_supplicant` tools.
- First we need to find out our wireless network device.
To do that we can type `ip a`. `Wlan*` or `wlp*s*` will be the one we are looking for.

- Now we need to configure `ifupdown interfaces`.
Open the `/etc/network/interfaces` and type the following:
```
  auto wlp*s*
  iface wlp*s* inet dhcp
      wpa-conf /tmp/ws.conf
```
This tells the `ifup` command to start the `wlp*s*` interface and use the `wpa_supplicant` tools.

- But before that, we need to specify which network we want to connect to and its password.
It can be easily done by `wpa_passphrase "Your Wi-Fi SSID" "Your Wi-Fi pw" > /tmp/ws.conf`.
As you can see, we use the same `/tmp/ws.conf` as in `/etc/network/interfaces`.

- Now we are ready to connect.
Run `ifup wlp*s*`. This command will connect to your AP by using `wpa_supplicant`, then receive an IP by `dhcpcd`.

- Test your connection.
`ping google.com`

- Troubleshooting.
TO DO
