# Arch Linux Config

OS and programs configuration after arch linux installation

# Audio

## PulseAudio
Program which controls audio (might use only amixer in future)

### Installation
```
sudo pacman -S pulseaudio
```

### Setting keybinds

List audio outputs
```
pactl list sinks short
```

Source: https://faq.i3wm.org/question/3747/enabling-multimedia-keys.1.html
Might be changed soon to amixer since pactl has no max volume limit
```
# Pulse Audio controls
bindsym XF86AudioRaiseVolume exec --no-startup-id pactl set-sink-volume 1 +5% #increase sound volume
bindsym XF86AudioLowerVolume exec --no-startup-id pactl set-sink-volume 1 -5% #decrease sound volume
bindsym XF86AudioMute exec --no-startup-id pactl set-sink-mute 1 toggle # mute sound
 
# Media player controls
bindsym XF86AudioPlay exec playerctl play
bindsym XF86AudioPause exec playerctl pause
bindsym XF86AudioNext exec playerctl next
bindsym XF86AudioPrev exec playerctl previous
```

# Firefox
TODO: add firefox extensions and more info about config

## Installation
```
sudo pacman -S firefox
```

## Firefox font rendering fix
Fix for a really annoying font rendering issue when using specific fonts such as Hack
Source: https://bbs.archlinux.org/viewtopic.php?id=233984

Simply install package ttf-croscore
```
sudo pacman -S ttf-croscore
```

# vim

## vim pasting
TODO: setup and configs

