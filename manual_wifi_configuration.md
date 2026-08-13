# Manual Wi-Fi configuration (no NetworkManager)
**Tested on**: Debian 13(Live USB)

**Objective**: Configure a wireless interface without using NetworkManager, using the persitent Debian tools

# Prerequisites
- Your Wi-Fi SSID and password
- Live USB: [debian-live-13.6.0-amd64-standard.iso](https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/debian-live-13.6.0-amd64-standard.iso)
- Wireless device `wlp1s0`
- Wi-Fi SSID and password
- Tools: `wpa_supplicant`, `ifupdown`

# Configuration

## First approach
- Run `wpa_passphrase "Wi-Fi SSID" "Wi-Fi password" > /tmp/ws.conf`

- Create/Add next lines to `/etc/network/interfaces`
  ```
    auto wlp1s0
    iface wlp1s0 inet dhcp
      wpa-conf /tmp/ws.conf
  ```

- Run:
  - `ifup wlp1s0` to connect
  - `ifdown wlp1s0` to disconnect
