# libvirt
- VM Management

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



## Resources
- https://wiki.archlinux.org/title/libvirt
- https://www.youtube.com/watch?v=HfNKpT2jo7U&ab_channel=octetz
- https://www.youtube.com/watch?v=6435eNKpyYw&t=172s&ab_channel=octetz
- https://octetz.com/docs/2020/2020-05-06-linux-hypervisor-setup/
- https://wiki.libvirt.org/VirtualNetworking.html
