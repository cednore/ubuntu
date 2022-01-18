Atom
====

[Atom](https://atom.io) is a free and open-source text and source code editor for macOS, Linux, and Microsoft Windows
with support for plug-ins written in JavaScript, and embedded Git Control. Developed by GitHub, Atom is a desktop
application built using web technologies.

## Installation

```sh
# Insert Atom repository
wget -qO - https://packagecloud.io/AtomEditor/atom/gpgkey | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] https://packagecloud.io/AtomEditor/atom/any/ any main" > /etc/apt/sources.list.d/atom.list'
sudo apt update

# Install Atom
sudo apt install atom
```
