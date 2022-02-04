# Sublime Text

[Sublime Text](https://www.sublimetext.com) is a sophisticated text editor for code, markup and prose.

## Installation

```sh
# Install the GPG key
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

# Insert repository for stable channel (recommended)
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

# Insert repository for dev channel
echo "deb https://download.sublimetext.com/ apt/dev/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

# Update apt sources
sudo apt update

# Install Sublime Text
sudo apt install sublime-text
```
