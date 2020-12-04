# Arch Installation 

##  Creating Bootable USB

* `dd bs=4M if=path/to/archlinux.iso of=/dev/sdx oflag=sync`

## Boot the live environment 

* `ls /sys/firmware/efi/efivars`
	- If you don't get any error, you are good to go with UEFI

### Connect to internet 
	- WiFi
		+ `iwctl` recommended
		+ `wpa_supplicant -B -i interface_name -c <(wpa_passphrase MYSSID passphrase)

* Verify internet connection
	- `ip addr`
	- `ping -c 4 archlinux.org`


### Update the System Clock

* timedatectl set-ntp true

### Partition the disks

* `lsblk`

* use gdisk -- `gdisk /dev/sda`

```
sda      8:0    0 931.5G  0 disk 
├─sda1   8:1    0     1G  0 part /boot/efi
├─sda2   8:2    0     2G  0 part [SWAP]
├─sda3   8:3    0    20G  0 part /
└─sda4   8:4    0 908.5G  0 part /home
```

* Format partition
	- mkfs.ext4, mkfs.fat -F32, mkswap

* Mount the partitions
	- `mount /dev/sda3 /mnt`
	- `mkdir -p /mnt/boot/efi /mnt/home`
	- `mount /dev/sda1 /mnt/boot/efi`
	- `mount /dev/sda4 /mnt/home`

### Installation 

* Find fastest mirror
	- `reflector -c Germany -a 12 --sort rate --save /etc/pacman.d/mirrorlist`
	- `pacman -Syy`

* `pacstrap /mnt base linux linux-firmware`
* `pacman -S vim grub efibootmgr networkmanager network-manager-applet intel-ucode sudo vi`

### Configure the System

* ##### Fstab
	- Generate filesystem tables
		+ `genfstab -U  /mnt >> /mnt/etc/fstab`

* Leave live media and move to actual (new) system
	- arch-chroot /mnt

* ##### Timezone
	- set timezone
		+ `ln -sf /usr/share/zoneinfo/Asia/Kolkata /etc/localtime`
		+ `hwclock --systohc`

* ##### Localization 
	- `vim /etc/locale.gen` and uncomment `en_US.UTF-8 UTF-8`
	- `locale-gen`
	- `vim /etc/locale.conf` and add `LANG=en_US.UTF-8`

* ##### Network Configuration
	- hostname - `vim /etc/hostname`
	- hosts - `vim /etc/hosts` -- add `127.0.0.1 localhost`

* ##### Root password
	- set root password - `passwd`

* ##### Bootloader
	- `pacman -S grub efibootmgr networkmanager` (network-manager-applet if GUI requried)
	- `grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB`
	- `grub-mkconfig -o /boot/grub/grub.cfg`


* ##### System services 
		- `systemctl enable NetworkManager`

* ##### User 
		- create user -  `useradd -m -U -c 'Bharathi M' -d /home/bharathi -s /bin/bash -G wheel bharathi`
		- set password - `passwd username`
			+ add user to wheel group - `usermod -aG username`
		-  Edit sudoers file 
			+ uncomment the wheel group line  
			+  `EDITOR=vim visudo`

* Exit for them the system - `exit`

* Unmount all mounts - `umount -a`

* Reboot the system 

***

## Setting up the system 

### Connect to network

* `nmtui` - for WiFi 
* Install Graphics driver
	- `mesa wireless_tools wpa_supplicant pulseaudio pavucontrol`
	- optional package:
		+ xf86-video-intel
* Install GUI
	- `xorg lightdm lightdm-gtk-greeter xfce4`

* Enable display manager
	- `Systemctl enable lightdm`

***

## Extra

* Optional 
	- edit grub file
		+ `vim /etc/default/grub`
	- generate grub.cfg
		+ `grub-mkconfig -o /boot/grub/grub.cfg`
	- `lspci -v`
