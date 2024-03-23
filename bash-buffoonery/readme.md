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


## Quick Total Bytes by type
```sh
find ~ -type f -exec wc -c {} \; | awk '{print $1}' | tr '\n' '+' | rev | cut -c1 --complement | rev | bc
```
- Get total bytes for type of file


## Auto-push on current repo
```sh
git push origin $(git branch --show-current)
```

### Resources
- https://linuxconfig.org/how-to-manage-wireless-connections-using-iwd-on-linux

## jq
```sh
cat test.json
``````out
{
  "rollingUpdate": {
    "maxSurge": "25%",
    "maxUnavailable": "25%"
  },
  "type": "RollingUpdate"
}
```

```sh
cat test.json | jq .type
``````out
"RollingUpdate"
```

## jpath (jsonpath) 
- kinda helpful, but `jq` is better : https://github.com/json-path/JsonPath

- if `test.json` looks like: 
```out
{
    "car": {
        "color": "blue",
        "price": "$20,000"
    },
    "bus": {
        "color": "white",
        "price": "$120,000"
    }
}
```

- then `cat test.json | jpath $.car.price` looks like:
```out
[
  "$20,000"
]
```


### Example 2
<details>
<summary>example test file</summary>

```
{
    "prizes": [
        {
            "year": "2018",
            "category": "physics",
            "overallMotivation": "\"for groundbreaking inventions in the field of laser physics\"",
            "laureates": [
                {
                    "id": "960",
                    "firstname": "Arthur",
                    "surname": "Ashkin",
                    "motivation": "\"for the optical tweezers and their application to biological systems\"",
                    "share": "2"
                },
                {
                    "id": "961",
                    "firstname": "Gérard",
                    "surname": "Mourou",
                    "motivation": "\"for their method of generating high-intensity, ultra-short optical pulses\"",
                    "share": "4"
                },
                {
                    "id": "962",
                    "firstname": "Donna",
                    "surname": "Strickland",
                    "motivation": "\"for their method of generating high-intensity, ultra-short optical pulses\"",
                    "share": "4"
                }
            ]
        },
        {
            "year": "2018",
            "category": "chemistry",
            "laureates": [
                {
                    "id": "963",
                    "firstname": "Frances H.",
                    "surname": "Arnold",
                    "motivation": "\"for the directed evolution of enzymes\"",
                    "share": "2"
                },
				  {
    "id": "914",
    "firstname": "Malala",
    "surname": "Yousafzai",
    "motivation": "\"for their struggle against the suppression of children and young people and for the right of all children to education\"",
    "share": "2"
  }
  ]
  }
  ]
  }

```

</details>

- Command
```sh
cat test-ex2.json | jpath '$.prizes.*.laureates[?(@.id=="914")]'
```

- Output

```out
[
  {
    "id": "914",
    "firstname": "Malala",
    "surname": "Yousafzai",
    "motivation": "\"for their struggle against the suppression of children and young people and for the right of all children to education\"",
    "share": "2"
  }
]
```
