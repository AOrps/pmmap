

## Searchsploit 
### Package: `exploitdb` 
### Location: `/usr/share/exploitdb`
### Usage
```sh
$ searchsploit remote smb microsoft windows

---------------------------------------------------------------- ---------------------------------
 Exploit Title                                                  |  Path
---------------------------------------------------------------- ---------------------------------
Microsoft DNS RPC Service - 'extractQuotedChar()' Remote Overfl | windows/remote/16366.rb
Microsoft Windows - 'EternalRomance'/'EternalSynergy'/'EternalC | windows/remote/43970.rb
Microsoft Windows - 'SMBGhost' Remote Code Execution            | windows/remote/48537.py
....

$ searchsploit -m windows/remote/43970.rb || searchsploit -m 43970

  Exploit: Microsoft Windows - 'srv2.sys' SMB Code Execution (Python) (MS09-050)
      URL: https://www.exploit-db.com/exploits/40280
     Path: /usr/share/exploitdb/exploits/windows/remote/40280.py
    Codes: CVE-2009-3103, CVE-2009-2532, CVE-2009-2526, MS09-050
 Verified: False
File Type: Python script, ASCII text executable
Copied to: /<LOC>/40280.rb

$ ls
43970.rb

```

## NSE Scripts (Enumeration)
### Package: `nmap`
### Location: `/usr/share/nmap/scripts`
