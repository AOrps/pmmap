# enum

## Shortlist (Table of Contents)

| Topic
|:-----------
| [Using Nmap](#nmap)
| [DNS](#dns)
| [SMB](#smb)
| [SMTP](#smtp)
| [SNMP](#snmp)
| [whois](#whois)

## nmap 

## dns
- Linux Tools: `host`,`dnsrecon`,`dnsenum`
- Windows Tools: `nslookup`

### Usage Linux
```sh
# host -t <query type> <zone>
host -t soa cf.com

# dnsrecon -d <zone>
dnsrecon cf.com

# dnsrecon -d <zone> -D <list> -t <type> # bruteforce scan with dnsrecon
dnsrecon -d cf.com -D ~/list.txt -t brt

# dnsenum <zone>
dnsenum cf.com
```

### Usage Window
```ps1
:: nsloopup <zone>
nslookup cf.com

:: nslookup -type=TXT <zone> <dns server> :: ~using the dns server to look for txt record of a zone
nslookup -type=TXT ops.cf.com 192.168.10.100
```


## smb

## smtp

## snmp

## whois
- info: domain name, name server, registrar

```bash
# template


# example
whois site.com -h 10.10.0.5 
```

