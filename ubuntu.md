# ubuntu

> My personal environment setup guide on Ubuntu

## Table of Contents

1. [Cloning this gist](#cloning-this-gist)
2. [Postinstall impish](#postinstall-impish)
   - [System tweaks](#system-tweaks)
   - [Basic apt packages](#basic-apt-packages)
   - [Shell setup](#shell-setup)
   - [Restore my dotfiles](#restore-my-dotfiles)
   - [Restore my SSH setup](#restore-my-ssh-setup)
   - [Restore my VPN setup](#restore-my-vpn-setup)
   - [Kill switch](#kill-switch)
   - [The Wonder Shaper](#the-wonder-shaper)
   - [OpenSSH server](#openssh-server)
   - [VNC server](#vnc-server)
   - [Samba server](#samba-server)
   - [Install fonts](#install-fonts)
   - [Favorite utilities](#favorite-utilities)
     - [Tilix](#tilix)
3. [Development atmosphere](#development-atmosphere)
   - [Linuxbrew](#linuxbrew)
   - [Node.js](#nodejs)
   - [Deno](#deno)
   - [PHP](#php)
   - [Hacklang](#hacklang)
   - [Python](#python)
   - [Ruby](#ruby)
   - [Golang](#golang)
   - [Rust](#rust)
   - [Terraform](#terraform)
   - [Ansible](#ansible)
   - [Docker](#docker)
   - [Kubernetes](#kubernetes)
   - [MongoDB](#mongodb)
   - [Takeout](#takeout)
   - [AWS CLI](#aws-cli)
   - [gcloud CLI](#gcloud-cli)
   - [Skaffold CLI](#skaffold-cli)
   - [Azure CLI](#azure-cli)
   - [LocalStack](#localstack)
   - [GitHub CLI](#github-cli)
   - [Okteto CLI](#okteto-cli)
   - [Doppler CLI](#doppler-cli)
   - [ngrok](#ngrok)
   - [Solana](#solana)
   - [Anchor](#anchor)
   - [Flow CLI](#flow-cli)
   - [Flyctl CLI](#flyctl-cli)
4. [Install apps](#install-apps)
   - [Google Chrome](#google-chrome)
   - [Microsoft Edge](#microsoft-edge)
   - [Opera](#opera)
   - [Visual Studio Code](#visual-studio-code)
   - [VSCodium](#vscodium)
   - [Sublime Text](#sublime-text)
   - [Sublime Merge](#sublime-merge)
   - [Atom](#atom)
   - [Notion Enhanced](#notion-enhanced)
   - [DBeaver](#dbeaver)
   - [k8slens](#k8slens)
   - [JetBrains Toolbox](#jetbrains-toolbox)
   - [AWS Client VPN](#aws-client-vpn)
   - [Amazon WorkSpaces client](#amazon-workspaces-client)
   - [AnyDesk](#anydesk)
   - [Skype for Linux](#skype-for-linux)
   - [Discord](#discord)
   - [Slack](#slack)
   - [Microsoft Teams](#microsoft-teams)
   - [Flatpak](#flatpak)
5. [GNOME setup](#gnome-setup)
   - [GNOME utilities](#gnome-utilities)
   - [My GNOME settings](#my-gnome-settings)
   - [My GNOME keybindings](#my-gnome-keybindings)
   - [My GNOME extensions](#my-gnome-extensions)
6. [Pre re-install OS](#pre-re-install-os)

## Cloning this gist

```bash
# Go inside personal workspace folder
mkdir -p ~/workspace/cednore && cd ~/workspace/cednore

# Clone this gist
git clone git@gist.github.com:65a11bef1fec40caef10e0a106fd4a4c.git ubuntu
```

## Postinstall impish

### System tweaks

```bash
# Keep deb files
echo 'Binary::apt::APT::Keep-Downloaded-Packages "true";' | sudo tee /etc/apt/apt.conf.d/01cache-deb

# Zero timeout on grub loader
sudo sed -i "s/quick_boot=\"1\"/quick_boot=\"0\"/g" /etc/grub.d/30_os-prober
sudo update-grub

# Kill snap
sudo apt autoremove --purge snapd gnome-software-plugin-snap
rm -rf ~/snap && sudo rm -rf /snap \
  /var/cache/snapd \
  /var/lib/snapd \
  /var/snap
sudo apt-mark hold snapd

# Increase swap file size
sudo swapoff /swapfile && sudo rm /swapfile
sudo dd if=/dev/zero of=/swapfile bs=1M count=32768
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo reboot

# Disable suspend and hibernation
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target

# Do nothing when closing lid
sudo sed -i "s/#HandleLidSwitch=suspend/HandleLidSwitch=ignore/g" /etc/systemd/logind.conf
sudo systemctl restart systemd-logind # this will freeze your desktop

# Remove default gnome games
sudo apt purge aisleriot gnome-mahjongg gnome-mines gnome-sudoku

# Remove thunderbird and rhythmbox (optional)
sudo apt purge "thunderbird*"
sudo apt purge "rhythmbox*"
```

### Basic apt packages

```bash
sudo apt install \
  git curl wget gettext gawk tree \
  gnupg gnupg2 ca-certificates lsb-release \
  software-properties-common apt-transport-https \
  build-essential \
  ufw net-tools nmap nethogs dnsmasq cifs-utils whois \
  tmux vim neovim \
  jq imagemagick ffmpeg \
  p7zip-full
```

### Shell setup

```bash
# Install zsh and change default shell as zsh
sudo apt install zsh
chsh -s $(which zsh)

# Install Oh My Zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Install Powerlevel10k
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

# Install zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# Install zsh-artisan
git clone https://github.com/jessarcher/zsh-artisan.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/artisan
```

### Restore my dotfiles

1. Follow the instructions in my `dotfiles` repo; https://github.com/cednore/dotfiles
2. Follow the instructions in my `.files` repo (private); https://github.com/cednore/.files
3. Restart shell after this

### Restore my SSH setup

Follow the instructions in my `ssh` repo (private); https://github.com/cednore/ssh

> **_INFO:_** Curious how to clone a private repo without ssh key? I have my GPG-encrypted (symmetrically
> password-protected) primary ssh key and OpenVPN client file shared on the wild internet. You can check them on my
> [Public Vault](https://tinyurl.com/cednore-public-vault) folder.

### Restore my VPN setup

Follow the instructions in my `ovpn-clients` repo (private); https://github.com/cednore/ovpn-clients

### Kill switch

```bash
# Environment setup (Commented out below env vars, assuming they are already set while restoring my VPN setup)
# export VPN_IP=""
# export VPN_PROTOCOL=""
# export VPN_PORT=""

# Disable IPv6
echo "net.ipv6.conf.all.disable_ipv6=1" | sudo tee -a /etc/sysctl.conf
echo "net.ipv6.conf.default.disable_ipv6=1" | sudo tee -a /etc/sysctl.conf
echo "net.ipv6.conf.lo.disable_ipv6=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
cat /proc/sys/net/ipv6/conf/all/disable_ipv6 # confirm if 1

# Disable IPv6 on ufw
sudo sed -i "s/IPV6=yes/IPV6=no/g" /etc/default/ufw

# Allow private network traffic
sudo ufw allow in to 10.0.0.0/8 && sudo ufw allow out to 10.0.0.0/8
sudo ufw allow in to 172.16.0.0/12 && sudo ufw allow out to 172.16.0.0/12
sudo ufw allow in to 192.168.0.0/16 && sudo ufw allow out to 192.168.0.0/16

# VPN kill switch
sudo ufw default deny outgoing && sudo ufw default deny incoming
sudo ufw allow out to $VPN_IP port $VPN_PORT proto $VPN_PROTOCOL
sudo ufw allow out on tun0 from any to any && sudo ufw allow in on tun0 from any to any

# Enable ufw
sudo ufw enable

# Confirm ufw status
sudo ufw status
```

### The Wonder Shaper

```bash
# Clone git repo and install as service
mkdir -p ~/workspace/cednore && cd ~/workspace/cednore
git clone https://github.com/cednore/wondershaper.git -b cednore-setup
cd wondershaper
sudo make install
sudo systemctl daemon-reload
sudo systemctl enable --now wondershaper.service
sudo systemctl restart wondershaper.service

# Edit conffile and restart service
sudo nano /etc/systemd/wondershaper.conf
sudo systemctl restart wondershaper.service
```

### OpenSSH server

```bash
# Install ssh server
sudo apt install openssh-server

# Allow ssh on firewall
sudo ufw allow ssh
```

### VNC server

```bash
# Replace `gnome-remote-desktop` with `x11vnc`
sudo apt purge gnome-remote-desktop && sudo apt install x11vnc

# Set vnc password
x11vnc -storepasswd $HOME/.vnc/passwd

# Create logfile
mkdir -p ~/.logs && touch ~/.logs/x11vnc.log

# Start the server
x11vnc -display $DISPLAY -forever -shared -rfbauth ~/.vnc/passwd -o ~/.logs/x11vnc.log
```

### Samba server

```bash
sudo apt update && sudo apt install samba
whereis samba
sudo smbpasswd -a $USER
sudo ufw allow samba
mkdir -p $HOME/Public && echo \
  "[public]\n\
  comment = Public files on $(cat /etc/hostname)\n\
  path = $HOME/Public\n\
  read only = no\n\
  browsable = yes" \
  | sudo tee -a /etc/samba/smb.conf
sudo service smbd restart
```

### Install fonts

```bash
# Basic fonts
sudo apt install fonts-hack fonts-firacode fonts-jetbrains-mono

# Install Meslo Nerd fonts
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/Meslo.zip
unzip Meslo.zip -d ~/.fonts
fc-cache -fv
rm Meslo.zip
```

### Favorite utilities

```bash
# Insert apt repositories
sudo add-apt-repository ppa:peek-developers/stable
sudo add-apt-repository ppa:christian-boxdoerfer/fsearch-daily
sudo add-apt-repository ppa:apandada1/blanket

# Install apt packages
sudo apt install \
  xclip \
  qrencode zbar-tools \
  filezilla \
  dconf-editor \
  synaptic \
  gnome-boxes \
  gnome-sound-recorder \
  flameshot peek \
  fsearch \
  blanket
```

#### Tilix

```bash
# Install
sudo apt install tilix

# Favorite settings
eval DEFAULT_TILIX_PROFILE=$(gsettings get com.gexperts.Tilix.ProfilesList default)
gsettings set com.gexperts.Tilix.Settings terminal-title-style 'none'
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ visible-name 'cednore'
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ default-size-columns 120
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ background-transparency-percent 12
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ font 'MesloLGS Nerd Font Mono 11'
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ background-color '#132738'
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ foreground-color '#FFFFFF'
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ palette "['#000000', '#FF0000', '#38DE21', '#FFE50A', '#1460D2', '#FF005D', '#00BBBB', '#BBBBBB', '#555555', '#F40E17', '#3BD01D', '#EDC809', '#5555FF', '#FF55FF', '#6AE3FA', '#FFFFFF']"
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ badge-color '#132738'
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ badge-color-set true
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ bold-color-set false
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ cursor-colors-set false
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ highlight-colors-set false
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ use-system-font false
gsettings set com.gexperts.Tilix.Profile:/com/gexperts/Tilix/profiles/$DEFAULT_TILIX_PROFILE/ use-theme-colors false
```

## Development atmosphere

### Linuxbrew

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> ~/.zshrc # Optional, already existing inside my dotfiles
```

### Node.js

```bash
# Install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash # Shell restart is required after this
nvm --version

# Install node 16.x
nvm install 16

# Install node 14.x
nvm install 14

# Set default node version as 14.x
nvm alias default 14

# Install yarn via npm
npm i yarn -g
```

### Deno

```bash
curl -fsSL https://deno.land/install.sh | sh
```

### PHP

```bash
# Insert Ondrej PHP PPA and install php 8.0 along with extensions
sudo add-apt-repository ppa:ondrej/php
sudo apt install php8.1
sudo apt install php8.1-curl php8.1-gd php8.1-xml php8.1-soap php8.1-mbstring php8.1-mysql php8.1-pgsql php8.1-zip php8.1-xdebug php8.1-dev

# Install composer
curl -sS https://getcomposer.org/installer -o composer-setup.php \
  && HASH=`curl -sS https://composer.github.io/installer.sig` \
  && php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
  && sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
  && rm composer-setup.php
echo 'export PATH="$HOME/.config/composer/vendor/bin:$PATH"' >> ~/.zshrc # Optional, already existing inside my dotfiles

# Set php 8.0 as default cli version
sudo update-alternatives --set php /usr/bin/php8.0
```

### Hacklang

```bash
sudo apt update
sudo apt install software-properties-common apt-transport-https
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xB4112585D386EB94

sudo add-apt-repository https://dl.hhvm.com/ubuntu
sudo apt update
sudo apt install hhvm
```

### Python

```bash
# Install python 3.x and pip
sudo apt install python3 python3-pip

# Python alias and PATH for global cli (optional, already existing inside my dotfiles)
echo "alias python=$(which python3)" >> ~/.zshrc
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
```

### Ruby

```bash
# Install rbenv
sudo apt install rbenv
rbenv init
echo 'eval "$(rbenv init -)"' >> ~/.zshrc # Optional, already existing inside my dotfiles

# Install ruby-build
mkdir -p "$(rbenv root)"/plugins && git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build

# Verify rbenv and ruby-build
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/main/bin/rbenv-doctor | bash

# Install ruby 3.0.3
rbenv install 3.0.3

# Set default ruby version
rbenv global 3.0.3

# Verify current ruby version
ruby -v
```

### Golang

```bash
sudo apt install golang-go
echo 'export PATH="$(go env GOPATH)/bin:$PATH"' >> ~/.zshrc # Optional, already existing inside my dotfiles
```

### Rust

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### Terraform

```bash
# Prerequisites
sudo apt update && sudo apt install gnupg software-properties-common curl

# Install Terraform CLI
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt update
sudo apt install terraform

# Install terraform autocomplete package
touch ~/.zshrc
terraform -install-autocomplete

# terraform-docs
go install github.com/terraform-docs/terraform-docs@v0.16.0

# terragrunt
brew install terragrunt
```

### Ansible

```bash
# Via pip
pip install ansible

# Via PPA
sudo add-apt-repository ppa:ansible/ansible
sudo apt install ansible
```

### Docker

```bash
# Uninstall old versions and ensure dependencies
sudo apt remove docker docker-engine docker.io containerd runc && sudo apt install ca-certificates curl gnupg lsb-release

# Install docker engine
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io

# Install docker-compose
pip install docker-compose

# Set docker group and add current user
sudo groupadd docker
sudo usermod -aG docker $USER

# Restart services and mark as startup
sudo systemctl restart docker.service
sudo systemctl restart containerd.service
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

### Kubernetes

```bash
# Prerequisites
sudo apt update && sudo apt install apt-transport-https ca-certificates curl

# kubectl, kubeadm, kubelet
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt update
sudo apt install kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl # pin versions

# kind
go install sigs.k8s.io/kind@v0.11.1

# minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# helm
curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt update
sudo apt install helm
```

### MongoDB

```bash
# Insert MongoDB CE repository
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
sudo apt update

# MongoDB meta package
sudo apt install mongodb-org

# mongo shell
sudo apt install mongodb-org-shell

# mongosh
sudo apt install mongodb-mongosh

# monogocli
sudo apt install mongocli
```

### Takeout

```bash
# Check docker installation
docker info

# Install Takeout cli
composer global require tightenco/takeout

# Set restart policy to `always` for all takeout containers
docker update --restart always $(docker ps -qa --filter "name=TO-")
```

### AWS CLI

```bash
# AWS CLI
pip install awscliv2
echo 'alias aws=awscliv2' >> ~/.zshrc # Optional, already existing inside my dotfiles

# AWS SAM CLI
pip install aws-sam-cli

# AWS Amplify CLI
npm install -g @aws-amplify/cli

# Configure AWS credentials and config
aws configure
```

### gcloud CLI

```bash
# Prerequisites
sudo apt install apt-transport-https ca-certificates gnupg

# Insert gcloud CLI repository
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo tee /usr/share/keyrings/cloud.google.gpg
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
sudo apt update

# Install gcloud CLI
sudo apt install google-cloud-cli

# Pin version
sudo apt-mark hold google-cloud-cli
```

### Skaffold CLI

```bash
gcloud components install skaffold
```

### Azure CLI

```bash
# Prerequisites
sudo apt update
sudo apt install ca-certificates curl apt-transport-https lsb-release gnupg

# Install Microsoft signing key
curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/microsoft.gpg > /dev/null

# Insert Azure CLI repository
echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/azure-cli.list
sudo apt update

# Install Azure CLI
sudo apt install azure-cli
```

### LocalStack

```bash
# Install localstack
pip install localstack

# Start localstack in detached mode
localstack start -d

# Check status
localstack status services
```

### GitHub CLI

```bash
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```

### Okteto CLI

```bash
curl https://get.okteto.com -sSfL | sh
```

### Doppler CLI

```bash
sudo apt update && sudo apt install apt-transport-https ca-certificates curl gnupg
curl -sLf --retry 3 --tlsv1.2 --proto "=https" 'https://packages.doppler.com/public/cli/gpg.DE2A7741A397C129.key' | sudo apt-key add -
echo "deb https://packages.doppler.com/public/cli/deb/debian any-version main" | sudo tee /etc/apt/sources.list.d/doppler-cli.list
sudo apt update && sudo apt install doppler
```

### ngrok

```bash
curl -s https://ngrok-agent.s3.amazonaws.com/ngrok.asc | sudo tee /etc/apt/trusted.gpg.d/ngrok.asc > /dev/null
echo "deb https://ngrok-agent.s3.amazonaws.com buster main" | sudo tee /etc/apt/sources.list.d/ngrok.list
sudo apt update
sudo apt install ngrok
```

## Solana

```bash
sh -c "$(curl -sSfL https://release.solana.com/v1.10.27/install)"
echo 'export PATH="$HOME/.local/share/solana/install/active_release/bin:$PATH"' >> ~/.zshrc # Optional, already existing inside my dotfiles
```

### Anchor

```bash
# Prerequisites
sudo apt update && sudo apt upgrade && sudo apt install pkg-config build-essential libudev-dev

# Install avm
cargo install --git https://github.com/project-serum/anchor avm --locked --force

# Install latest anchor version
avm install latest
avm use latest
```

### Flow CLI

```bash
sh -ci "$(curl -fsSL https://storage.googleapis.com/flow-cli/install.sh)"
```

### Flyctl CLI

```bash
curl -L https://fly.io/install.sh | sh
```

## Install apps

### Google Chrome

```bash
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | sudo tee /etc/apt/sources.list.d/google-chrome.list
sudo apt update
sudo apt install google-chrome-stable # or google-chrome-unstable, google-chrome-beta
```

### Microsoft Edge

```bash
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/edge stable main" > /etc/apt/sources.list.d/microsoft-edge-dev.list'
sudo rm microsoft.gpg
sudo apt update
sudo apt install microsoft-edge-stable # or microsoft-edge-beta, microsoft-edge-dev
```

### Opera

```bash
wget -qO- https://deb.opera.com/archive.key | gpg --dearmor | sudo dd of=/usr/share/keyrings/opera-browser.gpg
echo "deb [signed-by=/usr/share/keyrings/opera-browser.gpg] https://deb.opera.com/opera-stable/ stable non-free" | sudo dd of=/etc/apt/sources.list.d/opera-archive.list
sudo apt update
sudo apt install opera-stable # or opera-beta, opera-developer
```

### Visual Studio Code

```bash
# Install
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
rm -f packages.microsoft.gpg
sudo apt update
sudo apt install code # or code-insiders

# Fix "Visual Studio Code is unable to watch for file changes in this large workspace" (error ENOSPC)
echo 'fs.inotify.max_user_watches=524288' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

### VSCodium

```bash
wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg | gpg --dearmor | sudo dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg
echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main' | sudo tee /etc/apt/sources.list.d/vscodium.list
sudo apt update
sudo apt install codium
```

### Sublime Text

```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt update
sudo apt install sublime-text
```

### Sublime Merge

```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt update
sudo apt install sublime-merge
```

### Atom

```bash
wget -qO - https://packagecloud.io/AtomEditor/atom/gpgkey | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] https://packagecloud.io/AtomEditor/atom/any/ any main" > /etc/apt/sources.list.d/atom.list'
sudo apt update
sudo apt install atom
```

### Notion Enhanced

```bash
echo "deb [trusted=yes] https://apt.fury.io/notion-repackaged/ /" | sudo tee /etc/apt/sources.list.d/notion-repackaged.list
sudo apt update
sudo apt install notion-app-enhanced # or notion-app for just vanilla notion
```

### DBeaver

```bash
wget -O - https://dbeaver.io/debs/dbeaver.gpg.key | sudo apt-key add -
echo "deb https://dbeaver.io/debs/dbeaver-ce /" | sudo tee /etc/apt/sources.list.d/dbeaver.list
sudo apt update
sudo apt install dbeaver-ce
```

### k8slens

```bash
wget https://api.k8slens.dev/binaries/Lens-5.4.4-latest.20220325.1.amd64.deb
sudo apt install ./Lens-5.4.4-latest.20220325.1.amd64.deb
rm Lens-5.4.4-latest.20220325.1.amd64.deb
```

### JetBrains Toolbox

```bash
curl -fsSL https://raw.githubusercontent.com/nagygergo/jetbrains-toolbox-install/master/jetbrains-toolbox.sh | bash
```

### AWS Client VPN

```bash
wget -q -O - https://d20adtppz83p9s.cloudfront.net/GTK/latest/debian-repo/awsvpnclient_public_key.asc | sudo apt-key add -
echo "deb [arch=amd64] https://d20adtppz83p9s.cloudfront.net/GTK/latest/debian-repo ubuntu-20.04 main" | sudo tee /etc/apt/sources.list.d/aws-vpn-client.list
sudo apt update
sudo apt install awsvpnclient
```

### Amazon WorkSpaces client

```bash
wget -q -O - https://workspaces-client-linux-public-key.s3-us-west-2.amazonaws.com/ADB332E7.asc | sudo apt-key add -
echo "deb [arch=amd64] https://d3nt0h4h6pmmc4.cloudfront.net/ubuntu bionic main" | sudo tee /etc/apt/sources.list.d/amazon-workspaces-clients.list
sudo apt update
sudo apt install workspacesclient
```

### AnyDesk

```bash
# Prerequisites
sudo apt install libpangox-1.0-0

# Install AnyDesk app
wget -qO - https://keys.anydesk.com/repos/DEB-GPG-KEY | sudo apt-key add -
echo "deb http://deb.anydesk.com/ all main" | sudo tee /etc/apt/sources.list.d/anydesk-stable.list
sudo apt update
sudo apt install anydesk

# Disable auto-start
sudo systemctl disable anydesk.service
```

### Skype for Linux

```bash
curl -s https://repo.skype.com/data/SKYPE-GPG-KEY | sudo apt-key add -
echo "deb https://repo.skype.com/deb stable main" | sudo tee -a /etc/apt/sources.list.d/skype-stable.list
sudo apt update
sudo apt install skypeforlinux
```

### Discord

```bash
wget https://dl.discordapp.net/apps/linux/0.0.17/discord-0.0.17.deb
sudo apt install ./discord-0.0.17.deb
rm discord-0.0.17.deb
```

### Slack

```bash
curl -L https://packagecloud.io/slacktechnologies/slack/gpgkey | sudo apt-key add -
echo "deb https://packagecloud.io/slacktechnologies/slack/debian/ jessie main" | sudo tee -a /etc/apt/sources.list.d/slack.list
sudo apt update
sudo apt install slack-desktop
```

### Microsoft Teams

```bash
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/ms-teams stable main" > /etc/apt/sources.list.d/teams.list'
sudo apt update
sudo apt install teams
```

### Flatpak

```bash
# Install Flatpak
sudo apt install flatpak

# Install the Software Flatpak plugin
sudo apt install gnome-software-plugin-flatpak

# Add the Flathub repository
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

## GNOME setup

### GNOME utilities

```bash
sudo apt install gnome-tweaks gnome-shell-extensions wmctrl
killall -SIGQUIT gnome-shell # GNOME shell restart
```

### My GNOME settings

```bash
# Disable animations
gsettings set org.gnome.desktop.interface enable-animations false

# Show seconds on top center clock
gsettings set org.gnome.desktop.interface clock-show-seconds true

# Show weekday on top center clock
gsettings set org.gnome.desktop.interface clock-show-weekday true

# Show week numbers on calendar
gsettings set org.gnome.desktop.calendar show-weekdate true

# Dock at bottom of the screen
gsettings set org.gnome.shell.extensions.dash-to-dock dock-position 'BOTTOM'

# Static dock height
gsettings set org.gnome.shell.extensions.dash-to-dock extend-height false

# Fixed dock
gsettings set org.gnome.shell.extensions.dash-to-dock dock-fixed false

# Dock icon size
gsettings set org.gnome.shell.extensions.dash-to-dock dash-max-icon-size 52

# Mouse speed
gsettings set org.gnome.desktop.peripherals.mouse speed -0.8

# Disable middle-click paste
gsettings set org.gnome.desktop.interface gtk-enable-primary-paste false

# Workspaces on primary display only
gsettings set org.gnome.mutter workspaces-only-on-primary true

# Static workspaces
gsettings set org.gnome.mutter dynamic-workspaces false

# Only 3 workspaces
gsettings set org.gnome.desktop.wm.preferences num-workspaces 3

# Remove default bookmarks from Nautilus' left bar (reboot for changes to take effect)
sudo sed -i "s/DESKTOP=Desktop/#DESKTOP=Desktop/g" /etc/xdg/user-dirs.defaults
# sudo sed -i "s/DOWNLOAD=Downloads/#DOWNLOAD=Downloads/g" /etc/xdg/user-dirs.defaults
sudo sed -i "s/TEMPLATES=Templates/#TEMPLATES=Templates/g" /etc/xdg/user-dirs.defaults
# sudo sed -i "s/PUBLICSHARE=Public/#PUBLICSHARE=Public/g" /etc/xdg/user-dirs.defaults
# sudo sed -i "s/DOCUMENTS=Documents/#DOCUMENTS=Documents/g" /etc/xdg/user-dirs.defaults
sudo sed -i "s/MUSIC=Music/#MUSIC=Music/g" /etc/xdg/user-dirs.defaults
sudo sed -i "s/PICTURES=Pictures/#PICTURES=Pictures/g" /etc/xdg/user-dirs.defaults
sudo sed -i "s/VIDEOS=Videos/#VIDEOS=Videos/g" /etc/xdg/user-dirs.defaults
sed -i "s/XDG_DESKTOP_DIR/#XDG_DESKTOP_DIR/g" ~/.config/user-dirs.dirs
# sed -i "s/XDG_DOWNLOAD_DIR/#XDG_DOWNLOAD_DIR/g" ~/.config/user-dirs.dirs
sed -i "s/XDG_TEMPLATES_DIR/#XDG_TEMPLATES_DIR/g" ~/.config/user-dirs.dirs
# sed -i "s/XDG_PUBLICSHARE_DIR/#XDG_PUBLICSHARE_DIR/g" ~/.config/user-dirs.dirs
# sed -i "s/XDG_DOCUMENTS_DIR/#XDG_DOCUMENTS_DIR/g" ~/.config/user-dirs.dirs
sed -i "s/XDG_MUSIC_DIR/#XDG_MUSIC_DIR/g" ~/.config/user-dirs.dirs
sed -i "s/XDG_PICTURES_DIR/#XDG_PICTURES_DIR/g" ~/.config/user-dirs.dirs
sed -i "s/XDG_VIDEOS_DIR/#XDG_VIDEOS_DIR/g" ~/.config/user-dirs.dirs
```

### My GNOME keybindings

```bash
# Overriding default keybindings
gsettings set org.gnome.settings-daemon.plugins.media-keys home "['<Super>e']"
gsettings set org.gnome.mutter.keybindings toggle-tiled-left "[]"
gsettings set org.gnome.mutter.keybindings toggle-tiled-right "[]"
gsettings set org.gnome.desktop.wm.keybindings move-to-monitor-down "[]"
gsettings set org.gnome.desktop.wm.keybindings move-to-monitor-up "[]"
gsettings set org.gnome.desktop.wm.keybindings move-to-monitor-left "[]"
gsettings set org.gnome.desktop.wm.keybindings move-to-monitor-right "[]"
gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-left "['<Super>Left']"
gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-right "['<Super>Right']"
gsettings set org.gnome.desktop.wm.keybindings move-to-workspace-left "['<Primary><Super>Left']"
gsettings set org.gnome.desktop.wm.keybindings move-to-workspace-right "['<Primary><Super>Right']"

# Check current custom keybindings
gsettings get org.gnome.settings-daemon.plugins.media-keys custom-keybindings

# Create 5 custom keybindings
gsettings set org.gnome.settings-daemon.plugins.media-keys custom-keybindings \
  "[ \
    '/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom0/', \
    '/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom1/', \
    '/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom2/', \
    '/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom3/', \
    '/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom4/' \
  ]"

# Open TODO list (Super+G)
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom0/ name 'Open TODO list'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom0/ command 'gnome-todo'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom0/ binding '<Super>g'

# Launch terminal on Tilix (Super+T)
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom1/ name 'Launch terminal on Tilix'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom1/ command 'tilix'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom1/ binding '<Super>t'

# Screenshot by Flameshot (Ctrl+Super+Space)
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom2/ name 'Screenshot by Flameshot'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom2/ command 'flameshot gui'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom2/ binding '<Primary><Super>space'

# Screencast by Peek (Ctrl+Alt+Space)
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom3/ name 'Screencast by Peek'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom3/ command 'peek'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom3/ binding '<Primary><Alt>space'

# Toggle Mic (Super+B)
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom4/ name 'Toggle Mic'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom4/ command "bash $HOME/.scripts/toggle-mic.sh"
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom4/ binding '<Super>b'
```

### My GNOME extensions

```bash
# Built-in
gnome-extensions enable apps-menu@gnome-shell-extensions.gcampax.github.com
gnome-extensions enable drive-menu@gnome-shell-extensions.gcampax.github.com
gnome-extensions enable places-menu@gnome-shell-extensions.gcampax.github.com
gnome-extensions enable user-theme@gnome-shell-extensions.gcampax.github.com
gnome-extensions enable workspace-indicator@gnome-shell-extensions.gcampax.github.com
gnome-extensions enable ubuntu-appindicators@ubuntu.com
gnome-extensions enable ubuntu-dock@ubuntu.com
gnome-extensions enable ding@rastersoft.com

# Clipboard Indicator
git clone https://github.com/Tudmotu/gnome-shell-extension-clipboard-indicator.git ~/.local/share/gnome-shell/extensions/clipboard-indicator@tudmotu.com
killall -SIGQUIT gnome-shell
gnome-extensions enable clipboard-indicator@tudmotu.com

# Current screen only on window switcher
git clone https://github.com/mmai/Current_screen_only_on_window_switcher.git ~/.local/share/gnome-shell/extensions/Current_screen_only_for_Alternate_Tab@bourcereau.fr
killall -SIGQUIT gnome-shell
gnome-extensions enable Current_screen_only_for_Alternate_Tab@bourcereau.fr

# Pixel Saver
sudo apt install gnome-shell-extension-pixelsaver
killall -SIGQUIT gnome-shell
gnome-extensions enable pixel-saver@deadalnix.me
```

### Tweak nautilus

```bash
# code-nautilus
wget -qO- https://raw.githubusercontent.com/harry-cpp/code-nautilus/master/install.sh | bash
```

## Pre re-install OS

1. Backup dotfiles
2. Backup all Docker images

```bash
# Backup
docker save $(docker images -q) -o /path/to/save/dockers_images.tar
docker images | sed '1d' | awk '{print $1 " " $2 " " $3}' > dockers_images.list

# Restore
docker load -i /path/to/save/dockers_images.tar
while read REPOSITORY TAG IMAGE_ID
do
  echo "== Tagging $REPOSITORY $TAG $IMAGE_ID =="
  docker tag "$IMAGE_ID" "$REPOSITORY:$TAG"
done < dockers_images.list
```

3.
