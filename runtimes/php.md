PHP
===

[PHP](https://php.net) is a general-purpose scripting language geared towards web development. It was originally created
by Danish-Canadian programmer Rasmus Lerdorf in 1994. The PHP reference implementation is now produced by The PHP Group.

## Installation

```sh
# Insert Ondrej PHP PPA
sudo add-apt-repository ppa:ondrej/php

# Install php 8.0
sudo apt install php8.0

# Install common php 8.0 extensions
sudo apt install php8.0-curl php8.0-gd php8.0-xml php8.0-soap php8.0-mbstring \
    php8.0-mysql php8.0-pgsql php8.0-zip php8.0-xdebug php8.0-dev

# Install composer
curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && HASH=`curl -sS https://composer.github.io/installer.sig` \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
rm composer-setup.php

# Setup PATH for composer package binaries
echo 'export PATH="$HOME/.config/composer/vendor/bin:$PATH"' >> ~/.zshrc
```
