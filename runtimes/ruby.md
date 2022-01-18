Ruby
====

[Ruby](https://www.ruby-lang.org) is an interpreted, high-level, general-purpose programming language. It was designed
and developed in the mid-1990s by Yukihiro "Matz" Matsumoto in Japan. Ruby is dynamically typed and uses garbage
collection and just-in-time compilation.

## Installation

```sh
# Install rbenv
sudo apt install rbenv

# Init rbenv
rbenv init
echo 'eval "$(rbenv init -)"' >> ~/.zshrc # Restart shell after this

# Install ruby-build
mkdir -p "$(rbenv root)"/plugins
git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build

# Verify rbenv and ruby-build
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/main/bin/rbenv-doctor | bash

# Install ruby 3.0.3
rbenv install 3.0.3

# Set default ruby version
rbenv global 3.0.3

# Verify current ruby version
ruby -v
```
