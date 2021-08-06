# A list of essential software I personally need</br>

### You may need to enable 32-bit software support</br>
You need to modify **/etc/pacman.conf** by enabling **multilib** repo and then reinitialize pacman's database.</br>
-> **pacman -Syy**</br>

### Firefox and VLC</br>
-> **pacman -S firefox vlc**</br>

### rxvt-unicode terminal</br>
-> **pacman -S rxvt-unicode**</br>
Configuration is mostly taken from <a>https://addy-dclxvi.github.io/post/configuring-urxvt/</a>

~/.Xdefaults</br>
!! Colorscheme</br>

! special</br>
*.foreground: #93a1a1</br>
*.background: #141c21</br>
*.cursorColor: #afbfbf</br>

! black</br>
*.color0: #263640</br>
*.color8: #4a697d</br>

! red</br>
*.color1: #d12f2c</br>
*.color9: #fa3935</br>

! green</br>
*.color2: #819400</br>
*.color10: #a4bd00</br>

! yellow</br>
*.color3: #b08500</br>
*.color11: #d9a400</br>

! blue</br>
*.color4: #2587cc</br>
*.color12: #2ca2f5</br>

! magenta</br>
*.color5: #696ebf</br>
*.color13: #8086e8</br>

! cyan</br>
*.color6: #289c93</br>
*.color14: #33c5ba</br>

! white</br>
*.color7: #bfbaac</br>
*.color15: #fdf6e3</br>

!! URxvt Appearance</br>
URxvt.letterSpace: 0</br>
URxvt.lineSpace: 0</br>
URxvt.geometry: 92x24</br>
URxvt.internalBorder: 24</br>
URxvt.cursorBlink: true</br>
URxvt.cursorUnderline: false</br>
URxvt.saveline: 2048</br>
URxvt.scrollBar: false</br>
URxvt.scrollBar_right: false</br>
URxvt.urgentOnBell: true</br>
URxvt.depth: 24</br>
URxvt.iso14755: false</br>

URxvt.transparent: true</br>
URxvt.shading: 20</br>

### Zoom</br>
-> **git clone https://aur.archlinux.org/zoom.git**</br>
-> **cd zoom**</br>
-> **makepkg -si**</br>
