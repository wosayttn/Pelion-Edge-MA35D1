# Pelion-edge@MA35D1

## Building

Before building, you should install toolchain for MA35D1 first and register the poky toolchain environment.

```bash
# source /usr/local/oecore-x86_64/environment-setup-aarch64-poky-linux
```

### Mbed-edge Building

```bash
$ git clone https://github.com/wosayttn/mbed-edge
$ cd mbed-edge
$ git submodule update --init --recursive

<Replace your mbed_cloud_dev_credentials.c into config/>

$ ./build.sh
```

### Mbed-edge-example Building

```bash
$ git clone https://github.com/wosayttn/mbed-edge-examples
$ cd mbed-edge-examples
$ git submodule update --init --recursive

$ ./build.sh
```

## Execute on target board.

Make MA35D1 with internet accessable.

Copy neccessary executions to target side, then run.


```
root@ma35d1-evb:~# ifconfig
eth1      Link encap:Ethernet  HWaddr 00:11:22:33:44:66
          inet addr:192.168.15.178  Bcast:192.168.15.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:6631 errors:0 dropped:0 overruns:0 frame:0
          TX packets:410 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:436158 (425.9 KiB)  TX bytes:45255 (44.1 KiB)
          Interrupt:28

root@ma35d1-evb:~# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.15.254  0.0.0.0         UG    10     0        0 eth1
192.168.15.0    0.0.0.0         255.255.255.0   U     0      0        0 eth1
192.168.15.254  0.0.0.0         255.255.255.255 UH    10     0        0 eth1

root@ma35d1-evb:~# rm -rf /dev/random
root@ma35d1-evb:~# ln -s /dev/urandom /dev/random
root@ma35d1-evb:~# ./edge-core &
Generating random from /dev/random, this can take a long time!
2021-05-25 08:51:07.302 tid:    357 [ERR ][PAL ]: pal_loadSslSessionFromStorage
2021-05-25 08:51:08.290 tid:    357 [INFO][edgecc]: Edge-core got registered to

2021-05-25 08:51:08.290 tid:    357 [INFO][edgecc]: Endpoint id : 0179a2b8687000

root@ma35d1-evb:~# ./pt-example -n ma35d1
socket name is: /tmp/edge.sock
2021-05-25 08:52:03.093 tid:    369 [ERR ][rf  ]: Invalid parameters for read_fi
2021-05-25 08:52:03.093 tid:    369 [ERR ][tzone]: Could not read bytes from the
2021-05-25 08:52:08.094 tid:    369 [ERR ][rf  ]: Invalid parameters for read_fi
2021-05-25 08:52:08.095 tid:    369 [ERR ][tzone]: Could not read bytes from the

```

## Demo

<img src="/figures/PelionEdge_MA35D1.gif?raw=true">
