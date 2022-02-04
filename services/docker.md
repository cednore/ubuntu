# Docker

[Docker](https://www.docker.com) is a set of platform as a service products that use OS-level virtualization to deliver
software in packages called containers. Containers are isolated from one another and bundle their own software,
libraries and configuration files; they can communicate with each other through well-defined channels.

## Installation

```sh
# Uninstall old versions
sudo apt remove docker docker-engine docker.io containerd runc

# Prerequisites
sudo apt install ca-certificates curl gnupg lsb-release

# Insert Docker repository
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update

# Install docker engine
sudo apt install docker-ce docker-ce-cli containerd.io

# Install docker-compose
pip install docker-compose
```

## Postinstall

```sh
# Set docker group and add current user
sudo groupadd docker
sudo usermod -aG docker $USER

# Restart services and mark as startup
sudo systemctl restart docker.service
sudo systemctl restart containerd.service
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

## Known issues

```sh
# Fix name resolve error inside containers in Amazon Linux instances on AWS
echo '{"dns":["10.1.2.3","8.8.8.8"]}' | sudo tee /etc/docker/daemon.json
sudo systemctl restart docker
```
