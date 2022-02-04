# takeout

[Takeout](https://github.com/tighten/takeout) is a CLI tool for spinning up tiny Docker containers, one for each of your
development environment dependencies. It's meant to be paired with a tool like Laravel Valet. It's currently compatible
with macOS, Linux, Windows 10 and WSL2.

## Installation

```sh
# Check docker installation
docker info

# Install takeout cli
composer global require tightenco/takeout
```

## My setup

```sh
# Enable mysql container
takeout enable mysql

# Set restart policy to `always` for all takeout containers
docker update --restart always $(docker ps -qa --filter "name=TO-")
```
