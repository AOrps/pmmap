# Fixes

## ip and http
```
# add ip and domain to /etc/hosts
#echo '<ip> <domain>' | sudo tee -a /etc/hosts

echo '10.10.1.12' | sudo tee -a /etc/hosts
```
- `/etc/hosts` can be used to resolve an IP address to a fully qualified domain name (fqdn)

- Reference: 
  - https://blog.purestorage.com/purely-informational/what-is-the-etc-hosts-file-in-linux/
  - https://maddevs.io/writeups/hackthebox-devvortex/

## gzip
- **Decompress a gzip**
```
cd /usr/share/wordlists/
sudo gzip -d rockyou.txt.gz
```
