# Samba server

[Samba](https://www.samba.org) is a free software re-implementation of the SMB networking protocol, and was originally
developed by Andrew Tridgell. Samba provides file and print services for various Microsoft Windows clients and can
integrate with a Microsoft Windows Server domain, either as a Domain Controller or as a domain member.

## Installation

```sh
# Install samba server
sudo apt update
sudo apt install samba

# Confirm samba installation
whereis samba
```

## Configuration

```sh
# Set password for default user
sudo smbpasswd -a $USER

# Allow samba on ufw
sudo ufw allow samba
```

## Expose public folder

```sh
# Add a smb share target; [public]
mkdir $HOME/Public
echo "[public]\n\
    comment = Public files on $(cat /etc/hostname)\n\
    path = $HOME/Public\n\
    read only = no\n\
    browsable = yes" | sudo tee -a /etc/samba/smb.conf

# Restart samba daemon
sudo service smbd restart
```
