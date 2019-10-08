# Section 06 - Network Hacking - Gaining Access (WEP/WPA/WPA2 Cracking)

## WPA/WPA2 Cracking - How To Capture The Handshake

WPA/WPA2 fixes all the weaknesses in WEP. Packets contain no useful data. The only packets that can aid with the cracking process are the handshake packets. There are 4 packets sent when a client connects to the network.

This section focuses on capturing the handshake packets.

As usual, your wireless adapter must be in `Monitor` mode.

In one terminal, run `airodump-ng` against all the networks to identify your target.

Then run `airodump-ng` against the target network to capture packets with:
```bash
airodump-ng --bssid=<BSSID> --channel=<CH> --write=wpa_handshake $IFACE
```

Now literally sit down and wait for the handshake packets to be captured. This happens when a new client connects to the AP, so wait for a new client. Alternatively, you can use a deauthentication attack to disconnect an existing client and force it to reconnect automatically. This way you can intercept the handshake packets. For example, send 4 deauthentication packets (in a second terminal) with:

```bash
aireplay-ng --deauth=4 -a=<MAC_ADDRESS_OF_TARGET_NETWORK> -c=<MAC_ADDRESS_OF_CLIENT_TO_DISCONNECT> $IFACE
```

Note: `<MAC_ADDRESS_OF_CLIENT_TO_DISCONNECT>` can be retrieved from the `STATION` column of the second section of `airodump-ng`.

Sending only 4 packets instead of a very large numbers (like in section 17) will make the disconnection very short, thus transparent for the client. On the other hand, it is usually enough to intercept the handshake packets.

As a result, when the client connects again, `airodump-ng` displays a `WPA handhsake: xx:xx:xx:xx:xx:xx` message at the top of the first section.

As soon as this message shows up, you can now quit `airodump-ng` with `Ctrl+C`. The handshake packet is stored in `wpa_handshake`.
