# MongoDB

[MongoDB](https://www.mongodb.com) is a source-available cross-platform document-oriented database program. Classified
as a NoSQL database program, MongoDB uses JSON-like documents with optional schemas. MongoDB is developed by MongoDB
Inc. and licensed under the Server Side Public License.

## Installation

```sh
# Prerequisites
sudo apt install gnupg

# Insert MongoDB CE repository
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
sudo apt update

# Install MongoDB meta package
sudo apt install mongodb-org

# Install mongo shell
sudo apt install mongodb-org-shell

# Install monogocli
sudo apt install mongocli
```
