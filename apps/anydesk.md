# AnyDesk

[AnyDesk](https://anydesk.com) is a closed source remote desktop application distributed by AnyDesk Software GmbH. The
proprietary software program provides platform independent remote access to personal computers and other devices running
the host application.

## Installation

```sh
# Insert AnyDesk repository
wget -qO - https://keys.anydesk.com/repos/DEB-GPG-KEY | sudo apt-key add -
echo "deb http://deb.anydesk.com/ all main" | sudo tee /etc/apt/sources.list.d/anydesk-stable.list
sudo apt update

# Install AnyDesk
sudo apt install anydesk
```

## Tweaks

```sh
# Disalbe auto-start
sudo systemctl disable anydesk.service
```
