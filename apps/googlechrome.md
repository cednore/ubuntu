Google Chrome
=============

[Google Chrome](https://www.google.com/chrome) is a cross-platform web browser developed by Google.

## Installation

```sh
# Insert Google Chrome repository
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | sudo tee /etc/apt/sources.list.d/google-chrome.list
sudo apt update

# Install Google Chrome
sudo apt install google-chrome-stable
```

## Turning off auto-update

```sh
# Turn off Chrome browser updates
sudo touch /etc/default/google-chrome
echo "repo_add_once=false" | sudo tee -a /etc/default/google-chrome

# Turn off Chrome browser component updates (Optional)
echo '{"ComponentUpdatesEnabled":"false"}' | sudo tee /etc/opt/chrome/policies/managed/component_update.json
```
