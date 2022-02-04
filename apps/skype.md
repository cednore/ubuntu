# Skype for Linux

[Skype](https://www.skype.com) is a proprietary telecommunications application that specializes in providing VoIP-based
videotelephony, videoconferencing and voice calls. It also has instant messaging, file transfer, debit-based calls to
landline and mobile telephones, and other features.

## Installation

```sh
# Insert Skype repository
curl -s https://repo.skype.com/data/SKYPE-GPG-KEY | sudo apt-key add -
echo "deb https://repo.skype.com/deb stable main" | sudo tee -a /etc/apt/sources.list.d/skype.list
sudo apt update

# Install Skype for Linux
sudo apt install skypeforlinux
```
