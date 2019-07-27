# i3 Configuration
Configure i3 on my Debian machine.

## Install i3

```bash
sudo apt-get update && sudo apt-get install -y i3
```

## Copy the config file

```bash
```

## Enable touchpad gestures

Check if `/etc/X11/xorg.conf.d/` directory exists or not. If not, create one.

```bash
vim /etc/X11/xorg.conf.d/90-touchpad.conf
```

Add the following lines:

```vim
Section "InputClass"
        Identifier "touchpad"
        MatchIsTouchpad "on"
        Driver "libinput"
        Option "Tapping" "on"
        Option "TappingButtonMap" "lrm"
        Option "NaturalScrolling" "on"
        Option "ScrollMethod" "twofinger"
EndSection
```
Logout for changes to appear.
[Source](https://cravencode.com/post/essentials/enable-tap-to-click-in-i3wm/)

## Make brightness control work again

```vim
sudo find /sys/ -type f -iname '*brightness*'
```
Make sure that your output device is present in `/sys/class/backlight`. If not, make a symlink to it.

```bash
sudo ln -s /sys/devices/pci0000:00/0000:00:02.0/drm/card0/card0-LVDS-1/intel_backlight  /sys/class/backlight
```
**NOTE**: The above path for the device may vary from system to system.

```bash
vim /etc/X11/xorg.conf.d/00-backlight.conf
```

```vim
  Section "Device"
        Identifier  "Intel Graphics" 
        Driver      "intel"
        Option      "Backlight"  "intel_backlight"
    EndSection
```
[Source](https://askubuntu.com/questions/715306/xbacklight-no-outputs-have-backlight-property-no-sys-class-backlight-folder)