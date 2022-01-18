System tweaks
=============

## Keep deb files

```sh
echo 'Binary::apt::APT::Keep-Downloaded-Packages "true";' | sudo tee /etc/apt/apt.conf.d/01cache-deb
```

## Zero timeout on grub loader

```sh
sudo sed -i "s/quick_boot=\"1\"/quick_boot=\"0\"/g" /etc/grub.d/30_os-prober
sudo update-grub
```

## Kill snap

```sh
# Remove package
sudo apt autoremove --purge snapd gnome-software-plugin-snap

# Remove cache, daemon and user data
rm -rf ~/snap
sudo rm -rf /snap
sudo rm -rf /var/cache/snapd
sudo rm -rf /var/lib/snapd
sudo rm -rf /var/snap

# Hold snapd installation forever
sudo apt-mark hold snapd
```

## Increase swap file size

```sh
# Disable swap and delete the swapfile
sudo swapoff /swapfile
sudo rm /swapfile

# Create new swap space
sudo dd if=/dev/zero of=/swapfile bs=1M count=32768 # 32 GB

# Set r/w permission
sudo chmod 600 /swapfile

# Format it to swap
sudo mkswap /swapfile

# Turn on swap
sudo swapon /swapfile

# Reboot machine
sudo reboot
```

## Power settings

```sh
# Disable suspend and hibernation
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target

# Do nothing when closing lid
sudo sed -i "s/#HandleLidSwitch=suspend/HandleLidSwitch=ignore/g" /etc/systemd/logind.conf
sudo systemctl restart systemd-logind # this will freeze your desktop
```

## Remove default gnome games

```sh
sudo apt purge aisleriot gnome-mahjongg gnome-mines gnome-sudoku
```

## Remove thunderbird and rhythmbox

```sh
sudo apt purge "thunderbird*"
sudo apt purge "rhythmbox*"
```
