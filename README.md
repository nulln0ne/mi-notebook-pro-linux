## Intel Graphics (modesetting driver)
- `/etc/X11/xorg.conf.d/20-modesetting.conf`
```
Section "Device"
    Identifier  "Intel Graphics"
    Driver      "modesetting"
    Option      "AccelMethod"    "glamor"
    Option      "DRI"            "2"
EndSection
```
- `/etc/environment`
```
LIBGL_DRI3_DISABLE=1
```

## Nvidia GPU
#### Intel Only
- `/etc/modprobe.d/nouveau.conf`
```
blacklist nouveau
blacklist nvidia
```
- `/etc/modprobe.d/bbswitch.conf`
```
options bbswitch load_state=0 unload_state=0
```

## Touchpad
- `/etc/X11/xorg.conf.d/20-touchpad.conf`
```
Section "InputClass"
        Identifier "libinput touchpad"
        Driver "libinput"
        MatchIsTouchpad "on"
        MatchDevicePath "/dev/input/event*"
        Option "Tapping" "on"
        Option "ClickMethod" "clickfinger"
        Option "NaturalScrolling" "true"
EndSection
```


## Display Calibration
Move [this icc profile](https://www.notebookcheck.net/uploads/tx_nbc2/NV156FHM_N61.icm "this icc profile") to `/usr/share/color/icc/colord`


## Intel CPU microcode
- First of all, you should install `intel-ucode` package
- Then, type this command:
```
iucode_tool -S --write-earlyfw=/boot/early_ucode.cpio /lib/firmware/intel-ucode/*
```

## GRUB config (with intel-ucode support)
- `/etc/default/grub`
```
GRUB_DEFAULT=0
GRUB_TIMEOUT=0
GRUB_DISTRIBUTOR="Void"
GRUB_CMDLINE_LINUX_DEFAULT="loglevel=4 slub_debug=P page_poison=1 i915.enable_dc=2 i915.enable_fbc=1 i915.fastboot=1 i915.enable_psr=0"
GRUB_TERMINAL_INPUT=console
GRUB_TERMINAL_OUTPUT=console
GRUB_EARLY_INITRD_LINUX_CUSTOM="ucode.cpio"
```
