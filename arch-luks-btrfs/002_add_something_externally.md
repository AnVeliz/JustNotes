# It might be you have forgottent to install something to your basic installation. That is how to fix it outside of the installed Arch Linux.</br>

### Mount the encrypted volume and all subvolemes (they might be necessary depending on what you are going to do)</br>
-> **cryptsetup open /dev/sda2 system**</br>
-> **o=defaults,x-mount.mkdir**</br>
-> **o_btrfs=$o,compress=lzo,ssd,noatime**</br>
-> **mount -t btrfs -o subvol=root,$o_btrfs LABEL=system /mnt**</br>
-> **mount -t btrfs -o subvol=home,$o_btrfs LABEL=system /mnt/home**</br>
-> **mount -t btrfs -o subvol=snapshots,$o_btrfs LABEL=system /mnt/.snapshots**</br>
-> **mount *DEVICE* /mnt/boot**</br>
E.g.: -> mount /dev/sda1 /mnt/boot</br>

### Install necessary software</br>
-> **pacstrap -i /mnt PACKAGES**</br>
E.g.: -> pacstrap -i /mnt wpa_supplicant wireless_tools net-tools dhcpcd lynx curl wget iputils</br>
