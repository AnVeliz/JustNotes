# Basic GUI installation (awesomewm)</br>

### Install the essential part of Xorg and awesomewm</br>
-> **sudo pacman -S xorg-server xorg-xinit xterm awesome**</br>

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
