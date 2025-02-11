# Section 05 - Network Hacking - Pre Connection Attacks

## Targeted Packet Sniffing Using `airodump-ng`

Identify your target network by its ESSID.

Target your network and write all the captured data to a file with:
```bash
airodump-ng --bssid=<BSSID> --channel=<CH> --write=test $IFACE
```

Note there is a new section with `BSSID`, `STATION`, `PWR`, `Rate`, `Lost`, `Frames` and `Probe` columns. This second section displays information about the devices connected to our target network.
- `STATION` is the MAC address of the device
- `PWR` is the signal strength of the device
- `Rate` is the speed
- `Lost` is the amount of data lost
- `Frames` is the number of packets received
- `Probe` indicates whether the device is probing for networks

Hit `Ctrl+C` and confirm the existence of 4 new files whose names start with `test`:
- `test-01.cap`
- `test-01.csv`
- `test-01.kismet.csv`
- `test-01.kismet.netxml`

They contain everything that was sent to and from the access point during the `airodump-ng` session.

Run `wireshark` and open `test-01.cap` to display the (possibly encrypted) packets.

The packets might look like gibberish if they are encrypted. However the `Source` column displays useful information regarding the devices connected to the target network, like the manufacturer and the MAC address (to match with the `STATION` or `BSSID` columns to determine whether the device is conected to the router or the router itself).
