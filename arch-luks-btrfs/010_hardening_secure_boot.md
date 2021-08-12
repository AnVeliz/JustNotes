# You may want to harden your installation a bit by adding Secure Boot support

### Install UEFI and signing tools
-> **pacman -S efitools sbsigntools**

### Create a Uniform Kernel
-> **objcopy \\</br>
    --add-section .osrel="/usr/lib/os-release" --change-section-vma .osrel=0x20000 \\</br>
    --add-section .cmdline="/proc/cmdline" --change-section-vma .cmdline=0x30000 \\</br>
    --add-section .splash="/usr/share/systemd/bootctl/splash-arch.bmp" --change-section-vma .splash=0x40000 \\</br>
    --add-section .linux="/boot/vmlinuz-linux" --change-section-vma .linux=0x2000000 \\</br>
    --add-section .initrd="/boot/initramfs.img" --change-section-vma .initrd=0x3000000 \\</br>
    "/usr/lib/systemd/boot/efi/linuxx64.efi.stub" "arch-unified-unsigned.efi"**

### Create certificates
-> **openssl req -new -x509 -newkey rsa:2048 -subj "/CN=SecureBoot PK/" -keyout PK.key -out PK.crt -days 3650 -nodes -sha256**</br>
-> **openssl req -new -x509 -newkey rsa:2048 -subj "/CN=SecureBoot KEK/" -keyout KEK.key -out KEK.crt -days 3650 -nodes -sha256**</br>
-> **openssl req -new -x509 -newkey rsa:2048 -subj "/CN=SecureBoot db/" -keyout db.key -out db.crt -days 3650 -nodes -sha256**</br>

-> **openssl x509 -in "PK.crt" -inform PEM -out PK.der -outform DER**</br>
-> **openssl x509 -in "KEK.crt" -inform PEM -out KEK.der -outform DER**</br>
-> **openssl x509 -in "db.crt" -inform PEM -out db.der -outform DER**</br>

### Create UEFI compatible signatures
-> **uudigen --random > GUID.txt**</br>

-> **sbsiglist --owner "$(< GUID.txt)" --type x509 --output PK.esl PK.der**</br>
-> **sbsiglist --owner "$(< GUID.txt)" --type x509 --output KEK.esl KEK.der**</br>
-> **sbsiglist --owner "$(< GUID.txt)" --type x509 --output db.esl db.der**</br>

-> **sbvarsign --key PK.key --cert PK.crt --output PK.auth PK PK.esl**</br>
-> **sbvarsign --key PK.key --cert PK.crt --output KEK.auth KEK KEK.esl**</br>
-> **sbvarsign --key KEK.key --cert KEK.crt --output db.auth PK db.esl**</br>

### Sign the Unified Kernel
-> **sbsign --key new_efi_vars/db.key --cert new_efi_vars/db.crt --output bootloader/arch-unified-signed.efi bootloader/arch-unified-unsigned.efi**</br>

### Copy the Unified Kernel to a proper location
-> **mkdir /boot/EFI/Linux**</br>
-> **cp bootloader/arch-unified-signed.efi /boot/EFI/Linux/**</br>

### Use UEFI as a bootloader
-> **efibootmgr --create --disk /dev/sda --part 1 --loader "\EFI\Linux\arch-unified-signed.efi" --label "My Arch System" --verbose**</br>

### Update UEFI variables. Step zero.
You need to remove all variables from your BIOS. Be careful since you can brake your computer doing this. More detailed information can be found in the official doc.

### Update UEFI db variable as the first step of variables update (choose one of the two approaches below)
-> **efi-updatevar -e -f db.esl db**</br>
-> **efi-updatevar -e -b /boot/EFI/Linux/arch-unified-unsigned.efi**</br>
Notes: It might be that the signed kernel can't be loading with a secure boot error. As an overcome, you can add your kernel hash to **db** variable.
However, you would need to add new hashes every time you update the kernel.

### Update UEFI KEK variable as the second step
-> **efi-updatevar -e -f KEK.esl KEK**</br>

### Update UEFI PK variable as the third step (it will lock UEFI to user mode)
-> **efi-updatevar -f PK.auth PK**</br>

