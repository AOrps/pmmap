# qemu

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
- Need `-cdrom <ISO>` for Initial Boot into desired ISO.


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


## Replaying/Recording
- `-icount` is not allowed with hardward virtualization, thus `-enable-kvm` flag (to boost speed) can't be invoked
