# .dotfiles

**A portion of some Arch Linux configs and tips.**

## Arch Linux tips

### **Disabling laptop beeper**

[Full guide (Arch Wiki)](https://wiki.archlinux.org/title/PC_speaker)

In short, create the file:

`/etc/modprobe.d/nobeep.conf`

```bash
blacklist pcspkr
blacklist snd_pcsp
```

---

### **Adding some keyboard layouts**

[Full guide with X config (Arch Linux)](https://wiki.archlinux.org/title/Xorg/Keyboard_configuration#Using_X_configuration_files)

For example, create a keyboard with **us** and **ru** layouts, switch by `Shift + Alt`.

Update the file:

`/etc/X11/xorg.conf.d/00-keyboard.conf`

```bash
Section "InputClass"
        Identifier "system-keyboard"
        MatchIsKeyboard "on"
        Option "XkbLayout" "us,ru"
        Option "XkbModel" "pc104"
        Option "XkbOptions" "grp:alt_shift_toggle"
EndSection
```

---

### **Displaying emoji correctly**

1. Install the fonts: `sudo pacman -S noto-fonts-emoji`

2. Create the file `/etc/fonts/conf.d/emoji.conf`

```xml
<?xml version="1.0"?>
  <!DOCTYPE fontconfig SYSTEM "fonts.dtd">
  <fontconfig>

   <alias>
     <family>sans-serif</family>
     <prefer>
       <family>//Preffered font//</family>
       <family>Noto Color Emoji</family>
       <family>Noto Emoji</family>
     </prefer>
   </alias>

   <alias>
     <family>serif</family>
     <prefer>
       <family>//Preffered font//</family>
       <family>Noto Color Emoji</family>
       <family>Noto Emoji</family>
     </prefer>
   </alias>

   <alias>
    <family>monospace</family>
    <prefer>
      <family>//Preffered font//</family>
      <family>Noto Color Emoji</family>
      <family>Noto Emoji</family>
     </prefer>
   </alias>

  </fontconfig>
```

3. Run `fc-cache -v`

---

### **Bluetooth in Arch**

[Full guide with Bluetooth (Arch Linux)](https://wiki.archlinux.org/title/bluetooth)

1. Install some packages: `sudo pacman -S bluez bluez-utils blueman`

2. Check that `btusb` (generic kernel BT module) is loaded: `lsmod | grep btusb`. If it is not, load it by `modprobe btusb`

3. Check that bluetooth sytstem service is active: `sudo systemctl status bluetooth`. If it is not, enable it by `sudo systemctl enable bluetooth`

4. For BT connections use CLI (`bluetoothctl`) or GUI (`blueman`)

---

### **Wrong time in Windows after Dual Boot with Arch**

The best fix for this problem is making Arch use local time: `timedatectl set-local-rtc 1 --adjust-system-clock`

---

### **Function keys not working properly**

[Full guide (Arch Linux)](https://wiki.archlinux.org/title/Apple_Keyboard#Function_keys_do_not_work)

1. Temporarily solution: `echo 2 >> /sys/module/hid_apple/parameters/fnmode`

2. Permanent solution: create/update the file `/etc/modprobe.d/hid_apple.conf`:

   ```conf
   options hid_apple fnmode=2
   ```

   Then regenerate the initramfs: `mkinitcpio -P`
