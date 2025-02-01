# Wireless LAN configuration

```bash
Example Configuration for Wi-Fi (wlan0)

network:
    version: 2
    wifis:
        wlan0:
            dhcp4: no
            addresses:
                - 192.168.1.100/24   # Replace with your desired static IP and subnet mask
            routes:
                - to: default
                  via: 192.168.1.1   # Replace with your router's IP address (default gateway)
            nameservers:
                addresses:
                    - 8.8.8.8       # Google DNS
                    - 8.8.4.4       # Google DNS
            access-points:
                "your-ssid":        # Replace with your Wi-Fi SSID
                    password: "your-password"  # Replace with your Wi-Fi password
```
