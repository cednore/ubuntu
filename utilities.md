# My favorite utilities

## Synaptic

Synaptic is a graphical package management tool based on GTK+ and APT. Synaptic enables you to install, upgrade and
remove software packages in a user friendly way.

```sh
sudo apt install synaptic
```

## Tilix

Tilix is a feature-rich tiling terminal emulator following the GNOME human interface design guidelines.

```sh
# Install Tilix
sudo apt install tilix

# Setup gogh-to-tilix theme generator (see https://github.com/isacikgoz/gogh-to-tilix)
git clone --recurse-submodules https://github.com/isacikgoz/gogh-to-tilix.git
cd gogh-to-tilix/
chmod +x install.sh
mkdir ~/.config/tilix/schemes -p
./install.sh ~/.config/tilix/schemes
cd ..
rm -rf gogh-to-tilix
```

## dconf Editor

simple configuration storage system - graphical editor

```sh
sudo apt install dconf-editor
```

## Flameshot

Flameshot is a powerful yet simple-to-use screenshot software.

```sh
sudo apt install flameshot
```

## Peek

Peek is a simple screen recorder. It is optimized for generating animated GIFs but you can also directly record to WebM
or MP4 if you prefer.

```sh
# Insert Peek stable PPA
sudo add-apt-repository ppa:peek-developers/stable

# Install Peek
sudo apt install peek
```

## FSearch

FSearch is a fast file search utility, based on GTK3. It supports regular expressions, wildcards, fast sorting, instant
results with millions of files and more.

```sh
# Insert FSearch PPA
sudo add-apt-repository ppa:christian-boxdoerfer/fsearch-daily

# Install FSearch
sudo apt install fsearch
```

## Boxes

[GNOME Boxes](https://wiki.gnome.org/Apps/Boxes) is a desktop client to view or use local virtual machines, remote
physical machines, or remote virtual machines. Boxes is intentionally simple and easy to use.

```sh
sudo apt install gnome-boxes
```

## Blanket

Improve focus and increase your productivity by listening to different sounds. Or allows you to fall asleep in a noisy
environment.

```sh
# Insert Blanket PPA
sudo add-apt-repository ppa:apandada1/blanket

# Install Blanket
sudo apt install blanket
```

## xclip

xclip is a command line utility that is designed to run on any system with an X11 implementation. It provides an
interface to X selections ("the clipboard") from the command line.

```sh
# Install xclip
sudo apt install xclip

# Alias pbcopy & pbpaste
echo "alias pbcopy='xclip -selection clipboard'" >> ~/.zshrc
echo "alias pbpaste='xclip -selection clipboard -o'" >> ~/.zshrc
```

## qrencode

Qrencode is a utility software using libqrencode to encode string data in a QR Code and save as a PNG or an EPS image.

```sh
# Install qrencode
sudo apt install qrencode

# Alias to generate QR code from given string and output on terminal
echo "alias qr='qrencode -m 2 -t utf8 <<< \"\$1\"'" >> ~/.zshrc

# Generate QR code from given string and save it as PNG file on clipboard.
echo "function qr2clip { qrencode \$1 -o - | xclip -selection clipboard -t image/png }" >> ~/.zshrc
```

## zbar-tools

ZBar is a library for scanning and decoding bar codes from various sources such as video streams, image files or raw
intensity sensors. It supports EAN-13/UPC-A, UPC-E, EAN-8, Code 128, Code 39, Interleaved 2 of 5 and QR Code.

```sh
sudo apt install zbar-tools
```
