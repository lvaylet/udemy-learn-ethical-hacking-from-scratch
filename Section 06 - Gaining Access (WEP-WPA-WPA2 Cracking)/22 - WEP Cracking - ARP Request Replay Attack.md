# Section 06 - Network Hacking - Gaining Access (WEP/WPA/WPA2 Cracking)

## WEP Cracking - ARP Request Replay Attack

This is the most reliable method to generate traffic, sniff packets and crack the key of a not-so-busy WEP network. It should work if you have a good signal strength and a good network adapter.

The idea is to:
- Wait for an ARP packet.
- Capture it and replay it (retransmit it). This causes the AP to produce another packet with a **new IV**.
- Keep doing this until we have enough IVs to crack the key.

Following up on the previous lab, make sure you are associated with the network. If unsure, associate again.

Then run `aireplay-ng` again in a separate terminal. The command is nearly the same as before, with only a few changes:
- Run an **ARP Replay** attack instead of a **Fake Authentication** attack
- Remove the number of times to perform the attack
- Replace the `-a` option with a `-b` option

```bash
aireplay-ng --arpreplay -b <MAC_ADDRESS_OF_TARGET_NETWORK> -h <MAC_ADDRESS_OF_ADAPTER> $IFACE
```

For example:
```bash
aireplay-ng --arpreplay -b 64:16:F0:EC:7B:F3 -h 48:5D:60:2A:45:25 $IFACE
```

As a result:
- `aireplay-ng` waits for an ARP packet
- As soon as it gets an ARP packet, the number of data packets should increase very quickly in the `airodump-ng` terminal because the ARP packet is getting replayed again and again.

Now just run `aircrack-ng` in a separate terminal to actually crack the key. You might need to associate again to do so.
```bash
aircrack-ng arpreplay-01.cap
```

The first attempts might fail. Just wait for the right number of packets. Cracking even a 128-bit key (26-digit) should only take 45000 or 5000 packets.
