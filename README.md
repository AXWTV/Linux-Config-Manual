# Linux-Config-Manual

<h2>Display Configuration</h2>

```bash
$ ps -e | grep Xorg
```

<h2>chack if xrandr is installed</h2>

```bash
$ xrandr
Screen 0: minimum 320 x 200, current 1920 x 1080, maximum 16384 x 16384
HDMI-1 connected primary 1920x1080+0+0 (normal left inverted right x axis y axis) 410mm x 230mm
   1366x768      59.79 +
   1920x1080     60.00*   59.94
   1280x1024     75.02
   1280x720      60.00    50.00    59.94
   1024x768      75.03    60.00
   800x600       75.00    60.32
   720x576       50.00
   720x576i      50.00
   720x480       60.00    59.94
   720x480i      60.00    59.94
   640x480       75.00    60.00    59.94
   720x400       70.08
DP-1 disconnected (normal left inverted right x axis y axis)

$ xrandr --output HDMI-1 --mode 1920x1080

$ touch .xprofile .profile .xinitrc

$ echo "#!/bin/bash" >> .profile .xprofile .xinitric
$ echo "xrandr --output HDMI-1 --mode 1920x1080" >> .profile .xprofile .xinitric

$ touch /etc/X11/xorg.conf.d/10-monitor.conf
```
<p>paste in /etc/X11/xorg.conf.d/10-monitor.conf</p>

```bash
Section "Monitor"
    Identifier    "HDMI1" 
    Option        "PreferredMode" "1920x1080"
    Option        "TargetRefresh" "60"
    Option        "Position" "0 0"
    Option        "Enable" "true"
EndSection 
```
<h3>gdm 1920x1080</h3>

```bash
sudo cp ~/.config/monitors.xml /var/lib/gdm/.config/monitors.xml 
```
<p>also add https://linuxreviews.org/HOWTO_fix_screen_tearing#:~:text=Intel%20iGPUs%5B,if%20it%27s%20new. also help full https://askubuntu.com/questions/1347160/screen-tearing-when-using-xrandr-and-x11vnc-on-ubuntu-20-04</p>

```bash
sudo vim /etc/X11/xorg.conf.d/20-intel-gpu.conf
```

<p>paste this in there
to find out the driver use: grep drivers /var/log/Xorg.0.log
</p>

```bsah
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "TearFree"  "true"
EndSection
```


<h3>After doing all that just</h3>

```bash
sudo reboot
```
<h3>Install</h3>

```bash
$ sudo <packet_manager> install arandr
e.g
   sudo apt install arandr
   sudo dnf install arandr
   sudo pacman -Ss arandr
```

<h3>Supported</h3>
<p>Debian, Ubuntu, Fedora, CentOS, ...</p>
<p>or use https://github.com/phillipberndt/autorandr</p>

<h2>Screen saver</h2>

<p>You can disable the screen saver feature with:</p>

```bash
sudo systemctl mask suspend.target && sudo systemctl mask sleep.target
```

<h2>GTK - Theme problems</h2>

```bash
$ touch $HOME/.gtkrc-2.0 $HOME/.config/gtk-3.0/settings.ini
```

<p>paste in $HOME/.gtkrc-2.0</p>

```bash
gtk-icon-theme-name = "Adwaita"
gtk-theme-name = "Adwaita"
gtk-font-name = "DejaVu Sans 11"
```

<p>paste in $HOME/.config/gtk-3.0/settings.ini</p>

```bash
[Settings]
gtk-icon-theme-name = Adwaita
gtk-theme-name = Adwaita
gtk-font-name = DejaVu Sans 11
gtk-application-prefer-dark-theme = true
```
<p>other themes https://github.com/catppuccin/gtk</p>
<p>more details in https://wiki.archlinux.org/index.php/GTK#Dark_theme_variant</p>


