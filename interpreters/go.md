Go
==

[Go](https://golang.org) is a statically typed, compiled programming language designed at Google by Robert Griesemer,
Rob Pike, and Ken Thompson. Go is syntactically similar to C, but with memory safety, garbage collection, structural
typing, and CSP-style concurrency.

## Installation

```sh
# Insert Golang Backports PPA
sudo add-apt-repository ppa:longsleep/golang-backports

# Install golang-go
sudo apt install golang-go
```

## Postinstall

```sh
# Setup PATH for golang package binaries
echo 'export PATH="$(go env GOPATH)/bin:$PATH"' >> ~/.zshrc
```
