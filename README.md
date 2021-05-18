# Pelion-Edge-MA35D1 (Testing)

## Setup Building Environment

- On Ubuntu and Debian
```bash
$ sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib \
   build-essential chrpath socat cpio python python3 python3-pip python3-pexpect \
     xz-utils debianutils iputils-ping libsdl1.2-dev xterm curl
$ sudo apt-get update
$ sudo apt install apt-transport-https ca-certificates curl software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## Build-up Docker
```bash
$ git clone https://github.com/OpenNuvoton/MA35D1_Docker_Script.git
$ cd docker-yocto
$ ./build.sh
Please enter absolute path for shared folders(eg:/home/<user name>) : EX: /home/nuvoton
$ ./join.sh
ma35d1_nuvoton
nuvoton@a24d9e06abe3:~$ cd ~/share
nuvoton@a24d9e06abe3:~$ cd yocto
```
- Usage: **MACHINE=\<machine\> DISTRO=\<distro\> source sources init-build-env \<build-dir\>**
    - **\<machine\>**    machine name
    - **\<distro\>**     distro name
    - **\<build-dir\>**  build directory

- Choose which **DISTRO** configuration you want to build
    - **nvt-ma35d1** (sources/meta-ma35d1/conf/distro/nvt-ma35d1.conf)
    - **nvt-ma35d1-directfb** (sources/meta-nua3500/conf/distro/
nvt-ma35d1-directfb.conf)

- Choose which **MACHINE** configuration you want to build
    - **ma35d1-evb** (sources/meta-ma35d1/conf/machine/ma35d1-evb.conf)
    - **ma35d1-iot** (sources/meta-ma35d1/conf/machine/ma35d1-iot.conf)

- Image

|  Name   | Target | Layer |
|  ----  | ----  | ---- |
| **core-image-minimal**  | A small image that only allows a device to boot | Poky |
| **nvt-image-qt5** | Builds ma35d1 image with qt5 | meta-ma35d1 |

## Using repo to get Nuvoton MA35D1 manifest in docker
```bash
nuvoton@a24d9e06abe3:~/share/yocto$ git config --global user.email "test@test.test.test"
nuvoton@a24d9e06abe3:~/share/yocto$ git config --global user.name "test"
nuvoton@a24d9e06abe3:~/share/yocto$ repo init -u git://github.com/OpenNuvoton/MA35D1_Yocto-v3.1.3.git -m meta-ma35d1/base/ma35d1.xml
nuvoton@a24d9e06abe3:~/share/yocto$ repo sync -j"$(nproc)"
nuvoton@a24d9e06abe3:~/share/yocto$ MACHINE=ma35d1-evb DISTRO=nvt-ma35d1 source sources/init-build-env build
nuvoton@a24d9e06abe3:~/share/yocto/build$ bitbake core-image-minimal
```
