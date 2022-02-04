# Python

[Python](https://www.python.org) is an interpreted high-level general-purpose programming language. Its design
philosophy emphasizes code readability with its use of significant indentation. Its language constructs as well as its
object-oriented approach aim to help programmers write clear, logical code for small and large-scale projects.

## Installation

```sh
# Setup deadsnakes PPA
sudo add-apt-repository ppa:deadsnakes/ppa

# Install python 3.x
sudo apt install python3

# Install pip
sudo apt install python3-pip

# Alias python3 to python
echo "alias python=$(which python3)" >> ~/.zshrc

# Setup PATH for python package binaries
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
```
