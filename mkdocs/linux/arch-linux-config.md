# Arch Linux Config

OS and programs configuration after arch linux installation

## Software installation and configuration


### PulseAudio
PulseAudio handles media controls while amixer handles volume

#### PulseAudio installation
```
sudo pacman -S pulseaudio
```

#### Setting keybinds

List audio outputs
```
pactl list sinks short
```

#### i3 config

!!! note ""
    Source: https://faq.i3wm.org/question/3747/enabling-multimedia-keys.1.html

```
# Amixer volume controls
bindsym XF86AudioRaiseVolume exec --no-startup-id amixer -q set Master 2%+ unmute #increase sound volume
bindsym XF86AudioLowerVolume exec --no-startup-id amixer -q set Master 2%- unmute #decrease sound volume

# Pulse Audio media player controls
bindsym XF86AudioMute exec --no-startup-id pactl set-sink-mute 1 toggle # mute sound
bindsym XF86AudioPlay exec playerctl play-pause
bindsym XF86AudioStop exec playerctl stop
bindsym XF86AudioNext exec playerctl next
bindsym XF86AudioPrev exec playerctl previous
```

### Firefox

#### Firefox installation
```
sudo pacman -S firefox
```

#### Extensions and config


### Monitor layout setup
TODO: xrandr



### KeepassXC
KeepassXC is a KeepassX fork which adds additional features such as yubico key support

!!! note ""
    Source: https://keepassxc.org/

#### KeepassXC installation
```
sudo pacman -S keepassxc
```

### Rofi
Replacement for dmenu

#### Rofi installation
```
sudo pacman -S rofi
```

#### rofi i3 config
```
bindsym $mod+d exec rofi -show run
```


## Configuration

### vim

#### vim pasting
TODO: setup and configs


## Troubleshooting

### Firefox font rendering issues
Fix for a really annoying font rendering issue when using specific fonts such as Hack

!!! note ""
    Source: https://bbs.archlinux.org/viewtopic.php?id=233984

Simply install package ttf-croscore
```
sudo pacman -S ttf-croscore
```