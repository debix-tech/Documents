# 📡 Ethernet (EQoS & FEC)  - i.MX8MP



## 📘 概述

本平台配置了两个千兆以太网控制器：

- **EQoS (Enhanced QoS Ethernet MAC)**：支持多队列调度、DMA 队列映射等特性。
- **FEC (Fast Ethernet Controller)**：标准 RGMII 接口，支持 Magic Packet 唤醒等



## 📂 驱动源码位置

✅ 1. EQoS 驱动（DesignWare EQOS）

`drivers\net\ethernet\stmicro\stmmac\stmmac_main.c`

✅ 2. FEC 驱动（NXP IMX FEC）

`drivers/net/ethernet/freescale/fec_main.c`



**使用测试1：**

1.up起网口

```shell
ifconfig ens33 up 
ifconfig ens34 up 
```

2.测试网络连通性

```shell
ping 8.8.8.8
```

🧪 网口压力测试工具（可选）

`iperf3` 带宽测试



**使用测试2：**

网口唤醒CPU

1.设置网口支持唤醒功能

> 	Supports Wake-on: g
> 	Wake-on: g

```shell
root@imx8mp-debix:~# ethtool -s ens34 wol g
root@imx8mp-debix:~# ethtool ens34
Settings for ens34:
	Supported ports: [ TP	 MII ]
	Supported link modes:   10baseT/Half 10baseT/Full
	                        100baseT/Half 100baseT/Full
	                        1000baseT/Full
	Supported pause frame use: Symmetric
	Supports auto-negotiation: Yes
	Supported FEC modes: Not reported
	Advertised link modes:  10baseT/Half 10baseT/Full
	                        100baseT/Half 100baseT/Full
	                        1000baseT/Full
	Advertised pause frame use: Symmetric
	Advertised auto-negotiation: Yes
	Advertised FEC modes: Not reported
	Link partner advertised link modes:  10baseT/Half 10baseT/Full
	                                     100baseT/Half 100baseT/Full
	                                     1000baseT/Full
	Link partner advertised pause frame use: Symmetric
	Link partner advertised auto-negotiation: Yes
	Link partner advertised FEC modes: Not reported
	Speed: 1000Mb/s
	Duplex: Full
	Auto-negotiation: on
	master-slave cfg: preferred slave
	master-slave status: slave
	Port: Twisted Pair
	PHYAD: 0
	Transceiver: external
	MDI-X: Unknown
	Supports Wake-on: g
	Wake-on: g
	Link detected: yes

```



2.查看IP地址和mac地址

```shell
root@imx8mp-debix:~# ifconfig
ens34: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.2.56  netmask 255.255.255.0  broadcast 192.168.2.255
        inet6 fe80::1207:23ff:fe6e:be6  prefixlen 64  scopeid 0x20<link>
        ether 10:07:23:6e:0b:e6  txqueuelen 1000  (Ethernet)
        RX packets 1126  bytes 132697 (129.5 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 192  bytes 18823 (18.3 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```



3.进入待机

```shell
root@imx8mp-debix:~# echo mem > /sys/power/state
[  934.957246] PM: suspend entry (deep)
[  934.961277] Filesystems sync: 0.000 seconds
[  934.966689] Freezing user space processes
[  934.972279] Freezing user space processes completed (elapsed 0.001 seconds)
[  934.979283] OOM killer disabled.
[  934.982518] Freezing remaining freezable tasks
[  934.988208] Freezing remaining freezable tasks completed (elapsed 0.001 seconds)
[  934.995631] printk: Suspending console(s) (use no_console_suspend to debug)

```

4.在电脑上面发送网络包唤醒

注意：需保证电脑和debix板子在同一个局域网内

电脑端发送：

```shell
wakeonlan -i 192.168.2.56 10:07:23:6e:0b:e6
```

发送之后会看到debix端会被唤醒

```shell
[  935.382694] Enabling non-boot CPUs ...
[  935.383112] Detected VIPT I-cache on CPU1
[  935.383163] GICv3: CPU1: found redistributor 1 region 0:0x00000000388a0000
[  935.383197] CPU1: Booted secondary processor 0x0000000001 [0x410fd034]
[  935.384960] CPU1 is up
[  935.385324] Detected VIPT I-cache on CPU2
[  935.385358] GICv3: CPU2: found redistributor 2 region 0:0x00000000388c0000
[  935.385380] CPU2: Booted secondary processor 0x0000000002 [0x410fd034]
....
....
[  939.102507] PM: resume devices took 3.712 seconds
[  939.335905] OOM killer enabled.
[  939.339050] Restarting tasks ... done.
[  939.352857] random: crng reseeded on system resumption
[  939.358086] PM: suspend exit

```

