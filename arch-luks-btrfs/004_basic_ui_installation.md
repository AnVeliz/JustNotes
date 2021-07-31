# Basic GUI installation (awesomewm)</br>

### Install the essential part of Xorg and awesomewm</br>
-> **sudo pacman -S xorg-server xorg-xinit xterm awesome**</br>

### Create a normal user of wheel group</br>
-> **useradd --create-home *USER_NAME***</br>
E.g.: -> useradd --create-home me</br>
-> **passwd *USER_NAME***</br>
E.g.: -> passwd me</br>
-> **usermod --append --groups wheel *USER_NAME***</br>
E.g.: -> usermod --append --groups wheel me</br>

### Add SUDO permissions to the user</br>
-> **EDITOR=nano visudo**</br>
Notes: we need to uncomment: **%wheel ALL=(ALL) ALL** and **%sudo ALL=(ALL) ALL**</br>

### Allow sudo to be called by users</br>
-> **chmod 4755 /usr/bin/sudo**</br>

### Install all fonts using AUR</br>
-> **su *USESR_NAME***</br>
E.g.: -> su me</br>
-> **pacman -S git**</br>
-> **git clone https://aur.archlinux.org/all-repository-fonts.git**</br>
-> **cd all-repository-fonts**</br>
-> **makepkg -si**</br>

### Set awesome to run as X UI</br>
For debugging purpose: -> **echo "exec awesome >> /tmp/awesome/stdout 2>> /tmp/awesome/stderr" > ~/.xinitrc**</br>
For production run: -> **echo "exec awesome" > ~/.xinitrc**</br>
Notes: .xinitrc should be created for every user
