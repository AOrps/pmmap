# Bash Buffoonery

## bc output to sorted by second field
```bash
echo "
105*1.6
168.0
65*2.5
162.5
85*2.5
212.5
50*3
150
95*1.75
166.25
110*1.5
165.0" | grep -v '*' | cat -b | sort -n -k2 -r | cat -b
```
- `grep -v '*'` is responsible for getting all the output that is not a calculation
- `cat -b` to enumerate the numbers there
- `sort -n -k2 -r` reverse sort (highest first) at second field (`-k2`) on numeric values (`-n`)
- `cat -b` to enumerate the line there

## ipv4 address on oneline with with `ip`
```bash
# template
# ip -f[amily] inet -o[neline] addr show <ifname>

ip -f inet -o addr show eth0
```

## Connecting to wifi using `iwd` / `iwctl`

### List networks around
```bash
iwctl station <interface> get-networks

# ex
iwctl station wlan0 get-networks
```

### Connect
```bash
iwctl station <interface> connect <ESSID> --passphrase <PASSWD>

# ex
iwctl station wlan0 connect arda --passphrase superhot
```

### Verify connection
```bash
iwctl staton <interface> show

# ex:
iwctl station wlan0 show
```

### Disconnecting from a network
```bash
iwctl station <interface> disconnect
```

### List known connections
```bash
iwctl known-networks list
```

### Forget a network
```bash
iwctl known-networks <ESSID> forget

# ex:
iwctl known-networks arda forget
```

### To see passwords of
```bash
# to list directory of known-networks creds
ls /var/lib/iwd

# to view creds of known-networks
cat /var/lib/iwd/arda.psk
```

- Be sure to use a privileged user


### Resources
- https://linuxconfig.org/how-to-manage-wireless-connections-using-iwd-on-linux