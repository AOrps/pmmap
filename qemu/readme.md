# qemu

## Installation or Removal (apt)

### Installation
```sh
sudo apt install qemu-system
```

### Removal
- To remove all qemu things
```sh
for p in $(apt list --installed 2>/dev/null | grep 'qemu' | cut -d'/' -f1); do sudo apt remove -y $s; done
```

## Create Image
### Template Command
```bash
qemu-img create -f qcow2 <IMAGE_NAME> <SIZE>
```

### Example
```bash
qemu-img create -f qcow2 obsd.img 20G
```
- 


## Initial Boot
### Template Command
```bash
qemu-system-x86_64 -m <RAM_MEMORY_SIZE> -enable-kvm -drive file=<IMAGE_NAME> -cdrom <DISTRO_ISO_FILE> -boot order=d -display sdl,gl=on
```

### Example 
```bash
qemu-system-x86_64 -m 1G -enable-kvm -drive file=obsd.img -cdrom openbsd-install73.iso -boot order=d -display sdl,gl=on
```
- Need `-cdrom <ISO>` for Initial Boot into desired iso


## Boot (after initial boot)
### Example
```bash
qemu-system-x86_64 -enable-kvm -boot menu=on \
		   -drive file=obsd.img -m 8G -vga virtio \
		   -usb -device usb-tablet \
		   -display sdl,gl=on
```


## Snapshot
### Listing Snapshots
```bash
# Template
# qemu-img snapshot -l <IMAGE>

qemu-img snapshot -l obsd.img
```


### Adding a snapshot
```bash
# Template
# qemu-img snapshot -c <SNAPSHOT> <IMAGE>

qemu-img snapshot -c snap1 obsd.img
```

### Reverting to a Snapshot
```bash
# Template
# qemu-img snapshot -a <SNAPSHOT> <IMAGE>

qemu-img snapshot -a snap1 obsd.img
```

### Deleting a Snapshot
```bash
# Template
# qemu-img snapshot -d <SNAPSHOT> <IMAGE>

qemu-img snapshot -d snap1 obsd.img
```

### Resizing an image
```bash
# template
# qemu-img resize <img> <new_size>

qemu-img resize obsd.img 30G
```

## Networking

```bash
qemu-system-x86_64 -enable-kvm -boot menu=on \
		   -drive file=obsd.img -m 8G -vga virtio \
		   -usb -device usb-tablet \
		   -display sdl,gl=on \
           -device e1000,netdev=net0 \ 
           -netdev user,id=net0,hostfwd=tcp::5555-:22
           
# To Connect, ensure the vm has ssh service on and then you can ssh into the qemu vm:
# > ssh <qemu-user>@localhost -p 5555
```





- By default, the gateway router is the host machine 


### To list supported NIC models
```bash
qemu-system-x86_64 -nic model=help
```

## Cores that VM can use
- To check the number of cores, you can use the following commands:
  - linux: `nproc`
  - darwin, bsd: `sysctl -n hw.ncpu`
  - other: getconf _NPROCESSORS_ONLN

### Template
```bash
qemu-system-x86_64 -m <RAM_MEMORY_SIZE> -enable-kvm -cpu <CPU>  -smp <CORES> -drive file=<IMAGE_NAME> -cdrom <DISTRO_ISO_FILE> -boot order=d -display sdl,gl=on
```

### Example 
```bash
qemu-system-x86_64 -m 1G -enable-kvm -cpu host -smp 4 -drive file=obsd.img -cdrom openbsd-install73.iso -boot order=d -display sdl,gl=on

# alternatively can use something like this
qemu-system-x86_64 -m 1G -enable-kvm -cpu host -smp $(echo "$(nproc)//2" | bc | cut -d'.' -f1) -drive file=obsd.img -cdrom openbsd-install73.iso -boot order=d -display sdl,gl=on
```


### Resources
- https://stackoverflow.com/questions/45181115/portable-way-to-find-the-number-of-processors-cpus-in-a-shell-script



## Qemu Monitor

### Sending Keys to VM
- Sometimes you might need to send keys to the computer for certain functionality, it must be done via `compatmonitor0`
```keys
ctrl+alt+2

# ctrl-alt+f2 at login (on *nix), will force someone to work with terminal/text-based login/tty thing
# Within `compatmonitor0`, type:
(qemu) sendkey ctrl+alt+f2

# To switch back to `virtio-vga`, do:
ctrl+alt+1
```

### Snapshots

```keys
# Check existing snapshots

(qemu) info snapshots

# Create new snapshots
# template:
# (qemu) savevm <name>

(qemu) savevm new-test

# Load snapshots
# template:
# (qemu) loadvm <name>

(qemu) loadvm new-test

```

- Reference: https://wiki.qemu.org/Features/SnapshottingImprovements


## Device Passthrough 

### USB stick

- First check `lsusb`, `usbdevs` on openbsd. Might look something like this:
```
Bus 001 Device 003: ID 1111:aaaa -------- SOMETHING ---------
Bus 002 Device 004: ID 2222:cccc -------- SOMETHING ---------
Bus 003 Device 054: ID 3333:dddd          USB DISK
Bus 004 Device 123: ID 4444:ffff -------- SOMETHING ---------
...
```

- Shell Script `usb-devices` provides a lot more in depth knowledge about usb devices connected (as well as drivers)


- Let's say we want to pass-through the USB DISK, entry, the following might look like this:

```bash
# template 
cat << 'EOF
qemu-system-x86_64 -enable-kvm -boot menu=on \
		   -drive file=obsd.img -m 8G -vga virtio \
		   -display sdl,gl=on \
           -drive if=none,id=stick,format=raw,file=<.IMG file path> \
           -device nec-usb-xhci,id=xhci \
           -device usb-storage,bus=xhci.0,drive=stick \
           -usb -device usb-host,hostbus=<BUS ADDR>,hostaddr=<DEVICE ADDR>
EOF

qemu-system-x86_64 -enable-kvm -boot menu=on \
		   -drive file=obsd.img -m 8G -vga virtio \
		   -display sdl,gl=on \
           -drive if=none,id=stick,format=raw,file=/tmp/miniroot74.img \
           -device nec-usb-xhci,id=xhci \
           -device usb-storage,bus=xhci.0,drive=stick \
           -usb -device usb-host,hostbus=003,hostaddr=054

```

- Given that devices are at play here, one might need to use `sudo` or `doas` so it can read it from the host to the qemu vm

- Reference:
  - https://www.qemu.org/docs/master/system/devices/usb.html#connecting-usb-devices
  - https://www.qemu.org/docs/master/system/devices/usb.html#ehci-controller-support

## Replaying/Recording
- `-icount` is not allowed with hardward virtualization, thus `-enable-kvm` flag (to boost speed) can't be invoked
