# .dotfiles

**A portion of some Arch Linux configs and tips.**

## Arch Linux tips

---

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

### **Adding correctly visible emoji**

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
