# Microsoft Teams

[Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/group-chat-software) for Linux is your chat-centered
workspace in Office 365.

## Installation

```sh
# Install Microsoft Teams repository
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/ms-teams stable main" > /etc/apt/sources.list.d/teams.list'
sudo apt update

# Install Microsoft Teams
sudo apt install teams
```
