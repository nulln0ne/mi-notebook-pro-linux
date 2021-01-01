## Intel Graphics
#### Fix tearing
`/etc/X11/xorg.conf.d/20-intel.conf`

```
Section "Device"
  Identifier "Intel Graphics"
  Driver "intel"

  Option "TearFree" "true"
EndSection
```

#### Fix screen flickering
Enable kernel parameter `i915.enable_psr=0`

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
`/etc/X11/xorg.conf.d/20-touchpad.conf`
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
