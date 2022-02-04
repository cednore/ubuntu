# DBeaver

[DBeaver](https://dbeaver.io) is free and open source universal database tool for developers and database
administrators.

## Installation

```sh
# Insert DBeaver repository
wget -O - https://dbeaver.io/debs/dbeaver.gpg.key | sudo apt-key add -
echo "deb https://dbeaver.io/debs/dbeaver-ce /" | sudo tee /etc/apt/sources.list.d/dbeaver.list
sudo apt update

# Install DBeaver Community Edition
sudo apt install dbeaver-ce
```
