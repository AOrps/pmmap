# awk 

## Run a system command
```bash
# template
# awk '{system(CMD)}' <FILE>

awk '{system("host " $1 ".megacorpone.com")}' /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt 
# the command goes through the wordlist to enumerate ip address of the subdomain
```
