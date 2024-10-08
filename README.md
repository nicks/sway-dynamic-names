# i3-workspace-names-daemon

This script dynamically updates [sway](https://swaywm.org/) workspace names based on the names of the windows therein. 

It also allows users to define an icon to show for a named window from the [Font Awesome](https://origin.fontawesome.com/icons?d=gallery) icon list.

A rewrite of https://github.com/cboddy/i3-workspace-names-daemon built with sway in mind, although it should still work with i3.

## Examples
The workspace names in your bar of choice will look something like this:

<img src="https://raw.githubusercontent.com/cboddy/_vim_gifs/master/i3-bar-with-icons.png"></img>

## Install

### PIP

Install the [package](https://pypi.org/project/sway-dynamic-names/) from pypi with [pip](https://pypi.org/project/pip/).

```
sudo pip3 install sway-dynamic-names
```

**NB. if you don't have sudo privileges instead do**

```
pip3 install --user sway-dynamic-names
```

### Arch

Install the [package](https://aur.archlinux.org/packages/sway-dynamic-names-git/) using an aur helper like yay:

```
yay -S sway-dynamic-names-git
```

## Font 

Install the [Font Awesome](https://origin.fontawesome.com/icons?d=gallery) font via your favourite package manager. This is necessary if you want to show an icon instead of a window's name in the i3 status bar. 

### Debian/Ubuntu et al. 

```
sudo apt install fonts-font-awesome
```

### Arch

```
yay -S ttf-font-awesome
```

**NB: if the glyphs are not rendering make sure the font is installed.**


### Sway/i3 config

Add the following line to your `~/.config/sway/config`.

```
exec_always --no-startup-id exec sway-dynamic-names
```

If you use the ``$mod+1`` etc. shortcuts to switch workspaces then update the following so that the *switch to workspace* and *move focussed window to workspace* **shortcuts still work**. 


from 

```
bindsym $mod+1 workspace 1
bindsym $mod+Shift+1 move container to workspace 1
# etc
```

to

```
bindsym $mod+1 workspace number 1
bindsym $mod+Shift+1 move container to workspace number 1
# etc
```


## Configuration
Configuration is done in `~/.config/sway/sdn-config.yaml`. The default is:

```yaml
clients:
  google-chrome-beta: chrome
  jetbrains-pycharm: terminal
  firefox: firefox
  x-terminal-emulator: terminal
  thunderbird: envelope
  jetbrains-idea-ce: edit
  nautilus: folder-open
  clementine: music
  vlc: play
  signal: comment
deliminator: |
default_icon: dot-circle
```

### `clients`
A mapping of `client_identifier -> name`. The daemon will try and match the `client_identifier` against: 
`name`, `window_title`, `window_instance`, and `window_class`, as provided by sway, in that order. `client_identifier`
can also be a regular expression.

If `name` matches the name of a font-awesome icon, the icon will be used. Otherwise, any unicode symbol or plain text
can be used.

### `deliminator`

The symbol used to separate the names within a workspace

### `default_icon`

The icon to show if no windows in the workspace match the clients listed in the config

## Picking icons 

The easiest way to pick an icon is to search for one in the [gallery](https://origin.fontawesome.com/icons?d=gallery). **NB: the "pro" icons are not available in the debian/arch package.**

