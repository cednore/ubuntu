Flatpak
=======

[Flatpak](https://flatpak.org) is a utility for software deployment and package management for Linux. It is advertised
as offering a sandbox environment in which users can run application software in isolation from the rest of the system.
Flatpak was developed as part of the freedesktop.org project and was originally called xdg-app.

## Installation

```sh
# Install Flatpak
sudo apt install flatpak

# Install the Software Flatpak plugin
sudo apt install gnome-software-plugin-flatpak

# Add the Flathub repository
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```
