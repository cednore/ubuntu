Signal
======

[Signal](https://signal.org) is a cross-platform centralized encrypted instant messaging service developed by the
non-profit Signal Technology Foundation and Signal Messenger LLC. Users can send one-to-one and group messages, which
can include files, voice notes, images and videos.

## Installation

```sh
# Insert Signal repository
wget -O- https://updates.signal.org/desktop/apt/keys.asc | gpg --dearmor > signal-desktop-keyring.gpg
cat signal-desktop-keyring.gpg | sudo tee -a /usr/share/keyrings/signal-desktop-keyring.gpg > /dev/null
echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/signal-desktop-keyring.gpg] https://updates.signal.org/desktop/apt xenial main' |\
  sudo tee -a /etc/apt/sources.list.d/signal-xenial.list
sudo apt update

# Install Signal Desktop
sudo apt install signal-desktop
```
