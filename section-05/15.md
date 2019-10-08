# Section 05 - Network Hacking - Pre Connection Attacks

## WiFi Bands - 2.4Ghz & 5 Ghz Frequencies

`airodump-ng` only displays networks whose frequency band is supported by the wireless adapter, as displayed by `iwconfig`.

Sniff packets on 5Ghz with:
```bash
airodump-ng --band=a $IFACE
```

Capture packets on both 2.4Ghz and 5Ghz frequencies by specifying multiple bands with:
```bash
airodump-ng --band=abg $IFACE
```

Note that this requires a compatible wireless adapter, as well as more power and more resources.
