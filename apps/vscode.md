# Visual Studio Code & VSCodium

## Visual Studio Code

[Visual Studio Code](https://code.visualstudio.com) is a lightweight but powerful source code editor which runs on your
desktop and is available for Windows, macOS and Linux. It is an open-source project backed by Microsoft.

### Installation

```sh
# Insert Visual Studio Code repository
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
rm -f packages.microsoft.gpg
sudo apt update

# Install Visual Studio Code (recommended)
sudo apt install code

# Install Visual Studio Code Insiders
sudo apt install code-insiders
```

## VSCodium

[VSCodium](https://vscodium.com) is a community-driven, freely-licensed binary distribution of Microsoft’s editor
VSCode.

### Installation

```sh
# Insert VSCodium repository
wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg | gpg --dearmor | sudo dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg
echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main' | sudo tee /etc/apt/sources.list.d/vscodium.list
sudo apt update

# Install VSCodium
sudo apt install codium
```

## Known issues

```sh
# Fix "Visual Studio Code is unable to watch for file changes in this large workspace" (error ENOSPC)
echo 'fs.inotify.max_user_watches=524288' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```
