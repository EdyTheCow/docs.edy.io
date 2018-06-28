# Arch Linux

## Pre-Installation

!!! note ""
    Source: https://wiki.archlinux.org/index.php/Installation_guide

### Set keyboard to norwegian
```
loadkeys no-latin1
```

### Update the system clock
```
timedatectl set-ntp true
```

### Partition the disks
List all current partitions
```
fdisk -l
```

### Set partitions and swap

!!! note
    Replace [DISK] with one of disks listed in <b>fdisk -l</b> Example: sda

```
cfdisk /dev/[DISK]
```

Once disk is selected, create two partitions

| Size        | Type    | Bootable |
|-------------|---------|----------|
| All but 8GB | Default | Yes      |
| 8GB         | Swap    | No       |


### Format partitions

!!! warning
    Make sure to put <b>1</b> after the [DISK]. We're formatting a partition. Not the whole disk. (Same with swap)

```
mkfs.ext4 dev/[DISK]1
```

Setup swap
```
mkswap /dev/[DISK]2
```

```
swapon /dev/[DISK]2
```

## Installation

### Mount the disk
```
mount /dev/[DISK]1 /mnt
```

### Install base system
```
pacstrap -i /mnt base base-devel
```

## Configuration

### Generate fstab file
```
genfstab -U -p /mnt >> /mnt/etc/fstab
```

### Chroot
```
arch-chroot /mnt
```

### Set the clock
```
ln -sf /usr/share/zoneoinfo/Europe/Oslo /etc/localtime
```
```
hwclock --systohc
```

### Set locale
```
echo en_US.UTF-8 UTF-8 > /etc/locale.gen
```

```
locale-gen
```

```
echo LANG=en_US.UTF-8 > /etc/locale.conf
```

```
echo KEYMAP=no-latin1 > /etc/vconsole.conf
```

### Network configuration
```
echo moorch > /etc/hostname
```

```
echo "127.0.0.1	  localhost
::1		  localhost
127.0.1.1	  moorch.localdomain moorch" > /etc/hosts
```

## Grub

!!! note ""
    Source: https://wiki.archlinux.org/index.php/GRUB

### Install grub
```
pacman -S grub
```

```
grub-install --target=i386-pc /dev/[DISK]
```

```
grub-mkconfig -o /boot/grub/grub.cfg
```

Microcode
```
pacman -S intel-ucode 
```

```
grub-mkconfig -o /boot/grub/grub.cfg
```

### Set the root password
```
passwd
```

### Safely exit chroot

```
exit
```
```
umount /mnt
```

<b>Reboot the system</b>

## Post-Installation

### Internet connection
Often times there's no internet connection after installation. For a temporarily fix re-enable network interface.

!!! note
    Normally default interface is called eth0, but with smart naming enabled (default). It will be called eno1.

List current interfaces
```
ip link
```

Enable interface
```
dhcpcd eno1
```

### Update the system
```
pacman -Sy
```

### Add new user
```
useradd --create-home edy
```

Set password
```
passwd edy
```

Edit sudoers file
```
EDITOR=vim visudo
```

Add user under privileges section
```
edy ALL=(ALL) ALL
```

<b>Switch to newly created user</b>


### Network Manager

!!! note ""
    Source: https://wiki.archlinux.org/index.php/NetworkManager

Installing the package
```
sudo pacman -S networkmanager
```

Start the service
```
sudo systemctl start NetworkManager.service
```

Enable to start it on boot
```
sudo systemctl enable NetworkManager.service
```

### Aura package manager

!!! note ""
    Source: https://aur.archlinux.org/packages/aura-bin/

TODO:

- This needs to be cloned and then manually installed
- Alias auro with pacman so you can do -S for official and -A for AUR 
- Gist for more info

### Xorg

!!! note ""
    Source: https://wiki.archlinux.org/index.php/Xorg

Installation
```
sudo pacman -S xorg-server xorg-apps
```


#### Nvidia drivers

!!! note ""
    Source: https://wiki.archlinux.org/index.php/NVIDIA

Installation
```
sudo pacman -S nvidia
```

32-bit application support drivers
```
sudo pacman -S lib32-nvidia-utils lib32-nvidia-390xx-utils
```

<b>Reboot required</b>

Configure xorg
```
nvidia-xconfig
```

## i3-gaps

!!! note ""
    Source: https://i3wm.org/

Installation
```
```

Start xorg
```
startx
```

## Other resources
- https://wiki.archlinux.org/index.php/Network_configuration