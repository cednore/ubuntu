# ubuntu

> My personal environment setup for Ubuntu

## Getting started

```sh
# install python3
sudo apt install python3 python3-pip

# install ansible
pip install ansible

# download playbook

# if you have installed Ubuntu 20.04 (focal) on your PC
wget -O playbook.yml "https://raw.github.com/cednore/ubuntu/master/focal.yml"

# if you are using Ubuntu 20.04 (focal) on WSL
wget -O playbook.yml "https://raw.github.com/cednore/ubuntu/master/focal-wsl.yml"

# run playbook
ansible-playbook playbook.yml --ask-become-pass
```
