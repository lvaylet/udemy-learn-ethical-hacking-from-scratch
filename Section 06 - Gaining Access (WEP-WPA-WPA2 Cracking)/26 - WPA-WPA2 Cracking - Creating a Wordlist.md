# Section 06 - Network Hacking - Gaining Access (WEP/WPA/WPA2 Cracking)

## WPA/WPA2 Cracking - Creating a Wordlist

The handshake does **not** contain data that helps recover the key. It contains data that can be used to **check** if the key is valid or not.

We are going to create a very large collection of passwords and go through them one by one to confirm they are the key. You can download such lists from the internet but we are going to create our own list with a tool called `crunch`.

```bash
crunch [min] [max] [characters] -t [pattern] -o [filename]
```

For example, `crunch 6 8 123abc$ -o wordlist -t a@@@@b` generates:
```bash
aaaaab
aabbbb
aan$$b
...
```

Display more options with `man crunch`.
