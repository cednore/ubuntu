Amazon WorkSpaces
=================

[Amazon WorkSpaces](https://aws.amazon.com/workspaces) is a managed, secure Desktop-as-a-Service (DaaS) solution. You
can use Amazon WorkSpaces to provision either Windows or Linux desktops in just a few minutes and quickly scale to
provide thousands of desktops to workers across the globe.

## Installation

```sh
# Insert Amazon WorkSpaces Client repository
wget -q -O - https://workspaces-client-linux-public-key.s3-us-west-2.amazonaws.com/ADB332E7.asc | sudo apt-key add -
echo "deb [arch=amd64] https://d3nt0h4h6pmmc4.cloudfront.net/ubuntu bionic main" | sudo tee /etc/apt/sources.list.d/amazon-workspaces-clients.list
sudo apt update

# Install Amazon WorkSpaces
sudo apt install workspacesclient
```
