# Section 04 - Network Hacking

## Wireless Modes (Managed & Monitor)

Run `iwconfig` to display the wireless interfaces only, as well as their current mode.

First disable the wireless interface with:
```bash
IFACE=wlan1
ifconfig $IFACE down
```

Kill any process that could interfere with `Monitor` mode with:
```bash
airmon-ng check kill
````

Switch to `Monitor` mode with:
```bash
iwconfig $IFACE mode monitor
ifconfig $IFACE up
```

Confirm with:
```bash
iwconfig
```

Alternatively, you can use `airmon-ng` to switch to `Monitor` mode with:
```bash
airmong-ng start $IFACE
```

Note that the wireless adapter now shows up as `${IFACE}mon`, for example `wlan1mon`.
