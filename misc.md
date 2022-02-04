# Misc

## Install JetBrains Toolbox

```sh
curl -fsSL https://raw.githubusercontent.com/nagygergo/jetbrains-toolbox-install/master/jetbrains-toolbox.sh | bash
```

## Setting up VNC

```sh
# Remove
sudo apt purge gnome-remote-desktop

# Install x11vnc
sudo apt install x11vnc

# Set vnc password
x11vnc -storepasswd

# Start the server
x11vnc -display :0 -forever -shared -rfbauth ~/.vnc/passwd
```
