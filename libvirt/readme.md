# libvirt
- VM Management

## Compilation
- Building `libvirt` from scratch

### Cloning
- Clone the SSH location

### Builing (meta-compilation)
- To configure the type of building:
```sh
# Need to be in the root directory (and where the `meson.build` file is located)
meson configure
```

- Useful options to compile with
```sh
meson setup build -Dsystem=true -Ddriver_qemu=enabled -Ddriver_libvirtd=enabled -Dbash_completion=enabled -Dwireshark_dissector=enabled
```


- To update in order to update the build config, delete the `build` directory
```sh
rm -rf build/
```

#### Bash Completion
- On Ubuntu, be sure to install the following packages:
  - `libreadline-dev`


#### Wireshark Dissector 
- On Ubuntu, be sure to install the following packages: 
  - **`wireshark-dev`**
  - `libvirt-wireshark`
  - `libndpi-wireshark`
- In order to use the `wireshark_dissector` ensure that you are in the `wireshark` system group. In order to limit permissions to wireshark

### Compile
- To build the bianry
```sh
ninja -C build

# To add testing
ninja -C build test

# To add testing and use more cores
ninja -C build test -j$(nproc)
```

### Installing
- To install
```sh
sudo ninja -C build install
```

## Permissions
### Config Transfer
```sh
mkdir --parents ~/.config/libvirt
cp -rv /etc/libvirt/libvirt.conf ~/.config/libvirt/
```

- Update `~/.config/libvirt/libvirt.conf` to the following line uncommented to this:
```ini
uri_default = "qemu:///system"
```

- Change file owner and group of local copy
```sh
sudo chown $(whoami):$(groups | cut -d' ' -f1) ~/.config/libvirt/libvirt.conf
```

- Ensure you are in an administrator group in order for perms to do perms things.
  - `wheel` on arch, `sudo` on ubuntu


- Ensure you in `libvirtd` group on ubuntu: https://wiki.libvirt.org/Failed_to_connect_to_the_hypervisor.html

## Check the directory to add anything into it
```bash
# cd /var/lib/libvirt
# tree .

boot/           #
dnsmasq/        # dhcp 
images/         # where the vm images are stored (qcow2)
qemu/           
sanlock/
```
- Add `isos` dir to `/var/lib/libvirt`


## Ensure libvirtd is on
```
sudo systemctl status libvirtd

sudo systemctl restart libvirtd
```

## virt-install

### List ostypes (to prevent vm performance degradation)
```
virt-install --osinfo list 

# OR 

virt-install --os-variant list
```


### Debian Example
```bash
RAM=$((16 * 1024))

### ERRORS HERE
virt-install \
	--name deb0 \
	--memory ${RAM} \
	--disk path=/var/lib/libvirt/images/deb0.qcow2,size=20 \
	--vcpus 4 \
	--os-variant generic \
	--console pty,target_type=serial \
	--cdrom /var/lib/libvirt/isos/debian.iso
	
```


### List 


## virsh
### List domains
```bash
virsh list --all
```


### Start network
```bash
# sudo virsh net-start <network>
sudo virsh net-start default
```


## virt-manager
- GUI alternative to `virsh`

## virtqemu
- Check that `virtqemud` service is running
```sh
systemctl status virtqemud
```

## Issues
### virt-install: "This kernel requires an x86-64 CPU, but only detected an i686 CPU. Unable to boot – please use a kernel appropriate for your CPU"
- There might be an issue where qemu64 is not being recognized in libvirt on Ubuntu. 


### Not automatically restarting?
- Run the following command to get the path of the systemd service unit:
```sh
# it should be `/usr/local/lib/systemd/system/libvirtd.service`
systemctl status libvirtd
```
- Underneath `[Service]` area, append the following line:
```ini
RestartSec=3s
```

### Other issue resources
- https://askubuntu.com/questions/1225216/failed-to-connect-socket-to-var-run-libvirt-libvirt-sock
- https://libvirt.org/compiling.html
- https://wiki.libvirt.org/Failed_to_connect_to_the_hypervisor.html#other-errors
- https://unix.stackexchange.com/questions/715726/virsh-list-throw-error-failed-to-connect-socket-to-var-run-libvirt-virtqemud

## Resources
- https://wiki.archlinux.org/title/libvirt
- https://www.youtube.com/watch?v=HfNKpT2jo7U&ab_channel=octetz
- https://www.youtube.com/watch?v=6435eNKpyYw&t=172s&ab_channel=octetz
- https://octetz.com/docs/2020/2020-05-06-linux-hypervisor-setup/
- https://wiki.libvirt.org/VirtualNetworking.html

