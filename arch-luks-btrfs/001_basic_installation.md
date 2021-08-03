# The file contains commands which I entered to set up my basic Arch Linux configuration (UEFI system + LUKS + BTRFS + almost minimal Arch Linux).

### Connect to the Internet</br>
-> **wpa_passphrase *SSID* > /tmp/mywifi**</br>
E.g.: -> wpa_passphrase MyHomeWifiNet > /tmp/mywifi</br>
-> **wpa_supplicant -B -i *INTERFACE* -c /tmp/mywifi**</br>
E.g.: -> wpa_supplicant -B -i wlan0 -c /tmp/mywifi</br>
-> **dhcpcd *INTERFACE***</br>
E.g.: -> dhcpcd wlan0

### Check if we are in EFI mode</br>
-> **ls /sys/firmware/efi/efivars**</br>

### Disk partitioning</br>
-> **fdisk *DEVICE***</br>
E.g.: fdisk /dev/sda</br>
Notes: Make partitions N-Gb EFI (for boot) + the rest is Linux Filesystem</br>
-> **mkfs.vfat *DEVICE***</br>
E.g.: mkfs.vfat /dev/sda1</br>
-> **cryptsetup -y luksFormat --type luks2 *DEVICE***</br>
E.g.: cryptsetup -y luksFormat --type luks2 /dev/sda2</br>
-> **-> cryptsetup open *DEVICE* system**</br>
E.g.: -> cryptsetup open /dev/sda2 system</br>

### BTRFS partitioning</br>
-> **mkfs.btrfs --force --label system /dev/mapper/system**</br>
-> **mount -t btrfs LABEL=system /mnt**</br>
-> **btrfs subvolume create /mnt/root**</br>
-> **btrfs subvolume create /mnt/home**</br>
-> **btrfs subvolume create /mnt/snapshots**</br>
-> **umount -R /mnt**</br>

### Properly remount BTRFS partions</br>
-> **o=defaults,x-mount.mkdir**</br>
-> **o_btrfs=$o,compress=lzo,ssd,noatime**</br>
-> **mount -t btrfs -o subvol=root,$o_btrfs LABEL=system /mnt**</br>
-> **mount -t btrfs -o subvol=home,$o_btrfs LABEL=system /mnt/home**</br>
-> **mount -t btrfs -o subvol=snapshots,$o_btrfs LABEL=system /mnt/.snapshots**</br>

### Prepare /boot</br>
-> **mkdir /mnt/boot**</br>
-> **mount *DEVICE* /mnt/boot**</br>
E.g.: -> mount /dev/sda1 /mnt/boot</br>

### Prepare ArchLinux
-> **pacstrap -i /mnt base base-devel linux linux-firmware btrfs-progs nano vi vim git wpa_supplicant wireless_tools net-tools dhcpcd lynx curl wget iputils mc**</br>
Notes: the list of packages can be different later so you need to take a look at the official documentation. The list here is what I used to set up my system.</br>
-> **genfstab -p /mnt >> /mnt/etc/fstab**</br>
-> **arch-chroot /mnt**</br>
-> **ln -s /usr/share/zoneinfo/Europe/Brussels /etc/localtime**</br>
Note: choose your location</br>
-> **nano /etc/locale.gen**</br>
Note: Uncomment locales you need (I need only EN-US-UTF8)</br>
-> **locale-gen**</br>
-> **nano /etc/hostname**</br>
Note: Add your hostname here</br>
-> **nano /etc/mkinitcpio.conf**</br>
Note: in section "HOOKS" add "encrypt" before "filesystems"</br>
-> **mkinitcpio -p linux**</br>

### Change root password</br>
-> **passwd root**</br>
Note: You need to enter a new root password

### Set up bootloader, etc.
Note: Enter new root password</br>
-> **pacman -S grub efibootmgr**</br>
-> **nano /etc/default/grub**</br>
Notes:</br>
GRUB_ENABLE_CRYPTODISK=y</br>
GRUB_CMDLINE_LINUX="cryptdevice=/dev/sda2:system"</br>
-> **grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB**</br>
-> **grub-mkconfig -o /boot/grub/grub.cfg**

### Exit from installation</br>
-> **exit**</br>
-> **exit**</br>
-> **reboot**</br>

</br>
I've read a few articles and official documentation but always had some issues so nothing worked for me. That is why I decided to create a small set of notes compiled out of many articles (sorry, I don't remember which of them to refer because I copied commands to my sublimetext from there when I experimented with the installation and then assembled the file from what I had in sublimetext).
