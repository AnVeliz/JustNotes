# The final thing is to install audio device and other hardware related things</br>

### On my machine I need only to install audio</br>
-> **pacman -S alsa-utils pulseaudio pulseaudio-alsa pulseaudio-bluetooth pulseaudio-equalizer**</br>
-> **speaker-test**</br>
Notes: you may need to start **alsamixer** to set some extra settings and pulse equalizer **qpaeq**</br>

### Setting up touchpad tapping</br>
Edit files:</br>
- **/usr/share/X11/xorg.conf.d/*LIBINPUT_FILE***</br>
- **/usr/X11/xorg.conf.d/*LIBINPUT_FILE***</br>
where ***LIBINPUT_FILE*** is a  name of your local libinput configuration file (it has **libinput** in its name)</br>
Find touchpad settings section with **Driver "libinput"** setting and add there:</br>
**Option "Tapping" "on"**</br>
**Option "DisableWhileTyping" "on"**</br>

