# My GNOME settings

## Utilities

```sh
sudo apt install \
  gnome-tweaks \ # GNOME Tweak Tool
  wmctrl # Wmctrl
```

## Basic

```sh
# Disable animations
gsettings set org.gnome.desktop.interface enable-animations false

# Show weekday on top center clock
gsettings set org.gnome.desktop.interface clock-show-weekday true

# Show week numbers on calendar
gsettings set org.gnome.desktop.calendar show-weekdate true

# Favorite dock settings
gsettings set org.gnome.shell.extensions.dash-to-dock dock-position 'BOTTOM'
gsettings set org.gnome.shell.extensions.dash-to-dock extend-height false
gsettings set org.gnome.shell.extensions.dash-to-dock dock-fixed false
gsettings set org.gnome.shell.extensions.dash-to-dock dash-max-icon-size 52

# Mouse speed as -0.8
gsettings set org.gnome.desktop.peripherals.mouse speed -0.8

# Disable middle-click paste
gsettings set org.gnome.desktop.interface gtk-enable-primary-paste false
```

## Overriding default keybindings

```sh
gsettings set org.gnome.settings-daemon.plugins.media-keys home "['<Super>e']"
gsettings set org.gnome.mutter.keybindings toggle-tiled-left "[]"
gsettings set org.gnome.mutter.keybindings toggle-tiled-right "[]"
gsettings set org.gnome.desktop.wm.keybindings move-to-monitor-down "[]"
gsettings set org.gnome.desktop.wm.keybindings move-to-monitor-up "[]"
gsettings set org.gnome.desktop.wm.keybindings move-to-monitor-left "[]"
gsettings set org.gnome.desktop.wm.keybindings move-to-monitor-right "[]"
gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-left "['<Super>Left']"
gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-right "['<Super>Right']"
gsettings set org.gnome.desktop.wm.keybindings move-to-workspace-left "['<Primary><Super>Left']"
gsettings set org.gnome.desktop.wm.keybindings move-to-workspace-right "['<Primary><Super>Right']"
```

## Custom keybindings

```sh
# Check current keybindings
gsettings get org.gnome.settings-daemon.plugins.media-keys custom-keybindings

# Create 3 custom keybindings
gsettings set org.gnome.settings-daemon.plugins.media-keys custom-keybindings \
  "[ \
    '/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom0/', \
    '/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom1/', \
    '/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom2/' \
  ]"

# Launch terminal on Tilix (Super+T)
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom0/ name 'Launch terminal on Tilix'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom0/ command 'tilix'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom0/ binding '<Super>t'

# Screenshot by Flameshot (Ctrl+Super+Space)
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom1/ name 'Screenshot by Flameshot'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom1/ command 'flameshot gui'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom1/ binding '<Primary><Super>space'

# Screencast by Peek (Ctrl+Alt+Space)
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom2/ name 'Screencast by Peek'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom2/ command 'peek'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom2/ binding '<Primary><Alt>space'
```

## gnome-shell-extensions

Extensions to extend functionality of GNOME Shell.

```sh
# Install gnome-shell-extensions
sudo apt install gnome-shell-extensions # GNOME shell restart is required after this

# Enable user-theme extension
gnome-extensions enable user-theme@gnome-shell-extensions.gcampax.github.com
```

## Extensions

### GNOME Shell integration (Chrome Extension)

This extension provides integration with GNOME Shell and the corresponding extensions repository
https://extensions.gnome.org

1. Run following command to install native connector.

```sh
sudo apt install chrome-gnome-shell
```

2. Install chrome extension from this url;
   https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep

> You also can install connector manually. See
> https://wiki.gnome.org/Projects/GnomeShellIntegrationForChrome/Installation for install instructions.

### No Title Bar - Forked

> Extension URL; https://extensions.gnome.org/extension/2015/no-title-bar-forked
>
> Official Repo; https://github.com/poehlerj/no-title-bar

No Title Bar removes the title bar from non-GTK applications and moves the window title and buttons to the top panel.
Titlebars are also hidden for Wayland-native clients that don't use CSD. Some of the options may be incompatible with
this.

### Clipboard Indicator

> Extension URL; https://extensions.gnome.org/extension/779/clipboard-indicator
>
> Official Repo; https://github.com/Tudmotu/gnome-shell-extension-clipboard-indicator

Clipboard Manager extension for Gnome-Shell - Adds a clipboard indicator to the top panel, and caches clipboard history.

### Current screen only on window switcher

> Extension URL; https://extensions.gnome.org/extension/1437/current-screen-only-for-alternate-tab/
>
> Official Repo; https://github.com/mmai/Current_screen_only_on_window_switcher

Limits the windows shown on the switcher to those of the current monitor.

## Remove default bookmarks from Nautilus' left bar

```sh
sudo sed -i "s/DESKTOP=Desktop/#DESKTOP=Desktop/g" /etc/xdg/user-dirs.defaults
# sudo sed -i "s/DOWNLOAD=Downloads/#DOWNLOAD=Downloads/g" /etc/xdg/user-dirs.defaults
sudo sed -i "s/TEMPLATES=Templates/#TEMPLATES=Templates/g" /etc/xdg/user-dirs.defaults
# sudo sed -i "s/PUBLICSHARE=Public/#PUBLICSHARE=Public/g" /etc/xdg/user-dirs.defaults
# sudo sed -i "s/DOCUMENTS=Documents/#DOCUMENTS=Documents/g" /etc/xdg/user-dirs.defaults
sudo sed -i "s/MUSIC=Music/#MUSIC=Music/g" /etc/xdg/user-dirs.defaults
sudo sed -i "s/PICTURES=Pictures/#PICTURES=Pictures/g" /etc/xdg/user-dirs.defaults
sudo sed -i "s/VIDEOS=Videos/#VIDEOS=Videos/g" /etc/xdg/user-dirs.defaults

sed -i "s/XDG_DESKTOP_DIR/#XDG_DESKTOP_DIR/g" ~/.config/user-dirs.dirs
# sed -i "s/XDG_DOWNLOAD_DIR/#XDG_DOWNLOAD_DIR/g" ~/.config/user-dirs.dirs
sed -i "s/XDG_TEMPLATES_DIR/#XDG_TEMPLATES_DIR/g" ~/.config/user-dirs.dirs
# sed -i "s/XDG_PUBLICSHARE_DIR/#XDG_PUBLICSHARE_DIR/g" ~/.config/user-dirs.dirs
# sed -i "s/XDG_DOCUMENTS_DIR/#XDG_DOCUMENTS_DIR/g" ~/.config/user-dirs.dirs
sed -i "s/XDG_MUSIC_DIR/#XDG_MUSIC_DIR/g" ~/.config/user-dirs.dirs
sed -i "s/XDG_PICTURES_DIR/#XDG_PICTURES_DIR/g" ~/.config/user-dirs.dirs
sed -i "s/XDG_VIDEOS_DIR/#XDG_VIDEOS_DIR/g" ~/.config/user-dirs.dirs

# Reboot for changes to take effect
```

## Dynamic wallpapers

### Lakeside 2

```sh
# Install lakeside-2 dynamic wallpaper
curl -s https://wallpapers.manishk.dev/install.sh | bash -s Lakeside-2

# Then go to Settings -> Background and select Lakeside
```

> For more details, check out official [GitHub repo](https://github.com/manishprivet/dynamic-gnome-wallpapers).
