# Section 05 - Network Hacking - Pre Connection Attacks

## Packet Sniffing Basics Using `airodump-ng`

Switch to `Monitor` mode as instructed in Section 13.

Start sniffing packets with:
```bash
IFACE=wlan1
airodump-ng $IFACE
```

Let `airodump-ng` run for a few seconds then quit by hitting `Ctrl+C`.

The `ESSID` column shows the names of the wireless networks around us.

The other columns show additional details on these networks:
- `BSSID` shows us the MAC address of the target network
- `PWR` is the signal strength (power) of the network. The higher the number, the stronger the signal (even if negative).
- `Beacons` are frames sent by the network in order to broadcast its existence (even when it is set to hidden)
- `#Data` is the number of data packets or data frames (useful packets)
- `#/s` is the number of data packets collected in the past 10 seconds
- `CH` is the channel the network works on
- `MB` is the maximum speed supported by the network
- `ENC` is the encryption used by the network
- `CIPHER` is the cypher used in the network
- `AUTH` is the authentication used on this network
