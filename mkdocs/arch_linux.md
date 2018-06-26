# Arch Linux

## Installation

!!! note ""
    Source: https://wiki.archlinux.org/index.php/Installation_guide

Set keyboard to norwegian
```
loadkeys no-latin1
```

Update the system clock
```
timedatectl set-ntp true
```

List all current partitions
```
fdisk -l
```

Set partitions and swap

!!! note
    Replace [DRIVE] with one of drives listed in <b>fdisk -l</b> Example: sda

```
cfdisk /dev/[DRIVE]
```

Once drive is selected, create two partitions

| Size        | Type    | Bootable |
|-------------|---------|----------|
| All but 8GB | Default | Yes      |
| 8GB         | Swap    | No       |


Format partitions

!!! warning
    Make sure to put <b>1</b> after the [DRIVE]. We're formatting a partition. Not the whole drive. (Same with swap)

```
mkfs.ext4 dev/[DRIVE]1
```

Set swap
```
mkswap /dev/[DRIVE]2
```

```
swapon /dev/[DRIVE]2
```

Mount the drive
```
mount /dev/[DRIVE] /mnt
```

Install base system
```
pacstrap -i /mnt base base-devel
```

Generate fstab file
```
genfstab -U -p /mnt >> /mnt/etc/fstab
```

### Chroot

Chroot into the new system
```
arch-chroot /mnt
```

Set the clock
```
ln -sf /usr/share/zoneoinfo/Europe/Oslo /etc/localtime
```
```
hwclock --systohc
```

Set locale
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

Network configuration
```
echo moorch > /etc/hostname
```

```
echo "127.0.0.1	  localhost
::1		  localhost
127.0.1.1	  moorch.localdomain moorch" > /etc/hosts
```

### Grub

!!! note ""
    Source: https://wiki.archlinux.org/index.php/GRUB

Install grub
```
pacman -S grub
```

```
grub-install --target=i386-pc /dev/[DRIVE]
```

```
grub-mkconfig -o /boot/grub/grub.cfg
```

Set the root password
```
passwd
```

TODO:

- Microcode (https://wiki.archlinux.org/index.php/Microcode#Enabling_Intel_microcode_updates)
- Issues with internet connection (https://wiki.archlinux.org/index.php/Network_configuration)
- Package manager aura (https://aur.archlinux.org/packages/aura-bin/)
- Gist for more info

## i3-gaps