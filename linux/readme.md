# Linux


## Keybinds

| Hotkey | Key
| :----: | :-----
| `C`    | Control
| `M`    | ALT
| `^`    | Shift


| Keybind | Explanation
| :-----  | :--------
| `C-a`   | Jump to the start of the line
| `C-e`   | Jump to the end of the line



- Reference:
  - https://superuser.com/questions/362113/how-to-delete-all-characters-after-cursor-in-shell

## xorg things
- To check if a key produces input events:
```bash 
xev
```


## Audio (on Arch)



## Brightness (on Arch)



## OS
- Check `/etc/os-release`
```sh
cat /etc/os-release
```

- Run `uname`
```sh
uname
```

## systemd

### Figuring out Security Profile of a Unit
```sh
# template
# systemd-analyze security <service>.service

systemd-analyze security cups.service
```

### List systemd services (units)
```
systemctl list-units --type=service
```


## Package Managers

### Yum
- CentOS


- Installing a package: `yum install <pkg>`
- whatprovides: `yum whatprovides <pkg/binary>`

## Networking
- Routing Table: `route`
