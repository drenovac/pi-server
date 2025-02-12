# Developing in go on pi

## Installation

[Golang on Raspberry PI (Easiest)](https://d4v3y0rk.com/golang-on-rpi-easiest/)


Find the lastest release version tag, download the pkg, and install it
```bash
export GOPKG="$(curl -s https://api.github.com/repos/golang/go/git/matching-refs/tags/go | grep ref | grep -v url | grep -v beta | tail -1 | awk -F\/ {' print $3 '} | sed 's/",//')"
wget https://golang.org/dl/$GOPKG.linux-armv6l.tar.gz
sudo tar -C /usr/local -xzf $GOPKG.linux-armv6l.tar.gz
rm $GOPKG.linux-armv6l.tar.gz
Setup the shell
```
## for zsh
```bash

echo PATH=$PATH:/usr/local/go/bin >> $HOME/.zshrc
echo GOPATH=$HOME/golang >> $HOME/.zshrc
source $HOME/.zshrc
```
