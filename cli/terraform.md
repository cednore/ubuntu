# Terraform

[Terraform](https://www.terraform.io) is an open-source infrastructure as code software tool that provides a consistent
CLI workflow to manage hundreds of cloud services. Terraform codifies cloud APIs into declarative configuration files.

## Installation

```sh
# Prerequisites
sudo apt update && sudo apt install gnupg software-properties-common curl

# Insert HashiCorp Linux repository
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt update

# Install Terraform CLI
sudo apt install terraform
```

## Postinstall

```sh
# Install terraform autocomplete package
touch ~/.zshrc
terraform -install-autocomplete
```
