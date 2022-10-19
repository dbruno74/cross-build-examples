# Cross-build example

Some examples showing how to build an arm64 snap on a amd64 machine. 

## Prerequisites

LXD should be installed on your amd64 system
```
snap install lxd
lxd init
```
## Build procedure
### core20
```
lxc launch ubuntu:20.04 snapcraft-focal
cd core20
lxc file push test-confinement snapcraft-focal/root -p -r
lxc exec snapcraft-focal bash
cd test-confinement
apt update && apt upgrade
snap install snapcraft --classic
snapcraft --destructive-mode --target-arch=arm64 --enable-experimental-target-arch
```
### core22
```
cd core22/test-confinement
snapcraft --build-for=arm64
```
