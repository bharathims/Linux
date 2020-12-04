* Install required package
	- `sudo pacman -S virt-manager qemu ovmf vde2 ebtables dnsmasq bridge-utils openbsd-netcat`

* Enable and start the service
	- ` sudo systemctl enable libvirtd.service`
	- ` sudo systemctl start libvirtd.service`

* Add user to libvirt group
	- `sudo usermod -aG libvirt ${USER}`

* Check network interface status
	- `sudo virsh net-list --all`

* If it is inactive start it using
	-  `sudo virsh net-start default`


* What to do if default network interface is not listed

```
sudo virsh net-define /usr/share/libvirt/networks/default.xml
sudo virsh net-autostart default 
```


https://gist.github.com/diffficult/cb8c385e646466b2a3ff129ddb886185

*** 

## Exporting VM

* Export XML
	-sudo virsh dumpxml archlinux > archlinux.xml
		+ archlinux is a name of the virtual machine

* Find image 
	- cat archlinux.xml | grep  -i source

* cp the image
	- ex: `sudo dd if=vm_name.img of=Backup/vm_name.img bs=1M

### Clone VM 

* `sudo virt-clone --original archlinux --name arch --file ~/VMs/arch.img`

* `sudo virt-clone --original archlinux --name arch --file ~/VMs/Backup/arch.qcow2`

***

## Importing VM

* sudo virsh define ./mudkips.xml

***

*** 

## Snapchats 

* sudo virsh snapshot-create-as --domain {vm_name} --name {snapchat_name} --description "enter discritpion here"

### Tips and Trics

* List avilable virtual machines
	- `sudo virsh list --all`

* Start virtual machine 
	- `sudo virsh start vm_name`

* Stop virtula machine
	- `sudo virsh shutdown vm_name`

* Get IP address of the virtual machine
	- `sudo virsh net-list --all` -- get avilable networks
	-  `sudo virsh net-dhcp-leases default`
		+ default is a network name
