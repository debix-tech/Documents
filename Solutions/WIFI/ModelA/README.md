# 📶 brcmfmac WiFi Driver Usage Guide (i.MX8MP)

## 1. Overview

This system uses Broadcom’s brcmfmac series wireless chips (such as BCM43455 and BCM4356) to provide WiFi functionality. The driver is based on `brcmfmac`, and connects to the host via the `usdhc1` interface using SDIO communication.

## 2. Preparation

### 1. **Kernel Driver Modules**

Ensure the following kernel modules are enabled:

* `CONFIG_BRCMFMAC=m`
* `CONFIG_BRCMFMAC_SDIO=y`
* `CONFIG_CFG80211=y`
* `CONFIG_MAC80211=y`

Driver path:
`drivers/net/wireless/broadcom/brcm80211/brcmfmac`

### 2. **Firmware & NVRAM**

The firmware and calibration parameters (NVRAM) for the specific chip must be located under `/lib/firmware/brcm/`, for example:

```shell
root@imx8mp-debix:/lib/firmware/brcm# ls
BCM4345C0.hcd  BCM4345C5.hcd  brcmfmac43455-sdio.bin  brcmfmac43455-sdio.clm_blob  
brcmfmac43455-sdio.fsl,imx8mp-evk.txt  brcmfmac43456-sdio.bin  
brcmfmac43456-sdio.clm_blob  brcmfmac43456-sdio.fsl,imx8mp-evk.txt
```

---

## 3. Loading the Driver

At system startup, the kernel will automatically detect the WiFi chip on the SDIO bus and load the brcmfmac driver.

You can verify successful loading by checking the kernel log:

```shell
root@imx8mp-debix:/lib/firmware/brcm# dmesg | grep brcmfmac
[    9.935437] brcmfmac: brcmf_fw_alloc_request: using brcm/brcmfmac43455-sdio for chip BCM4345/6
[    9.935531] brcmfmac mmc0:0001:1: Direct firmware load for brcm/brcmfmac43455-sdio.fsl,imx8mp-evk.bin failed with error -2
[    9.935539] brcmfmac mmc0:0001:1: Falling back to sysfs fallback for: brcm/brcmfmac43455-sdio.fsl,imx8mp-evk.bin
[   10.108196] brcmfmac: brcmf_c_preinit_dcmds: Firmware: BCM4345/6 wl0: Sep 21 2018 04:08:34 version 7.45.173 (r707987 CY) FWID 01-d2799e
```

---

## 4. Network Configuration

### 1. Enable WiFi

```shell
root@imx8mp-debix:/lib/firmware/brcm# ifconfig wlan0 up
SIOCSIFFLAGS: Operation not possible due to RF-kill
root@imx8mp-debix:/lib/firmware/brcm# rfkill unblock all
root@imx8mp-debix:/lib/firmware/brcm# ifconfig wlan0 up
root@imx8mp-debix:/lib/firmware/brcm# ifconfig
...

wlan0: flags=-28669<UP,BROADCAST,MULTICAST,DYNAMIC>  mtu 1500  
        ether ac:6a:a3:23:b4:b5  txqueuelen 1000  (Ethernet)  
        RX packets 0  bytes 0 (0.0 B)  
        RX errors 0  dropped 0  overruns 0  frame 0  
        TX packets 0  bytes 0 (0.0 B)  
        TX errors 0  dropped 0  overruns 0  carrier 0  collisions 0  
```

### 2. Connect to a WiFi Network

```shell
root@imx8mp-debix:/lib/firmware/brcm# wpa_passphrase BH123 1234567890 >> /etc/wpa_supplicant.conf
root@imx8mp-debix:/lib/firmware/brcm# wpa_supplicant -Dnl80211 -iwlan0 -c/etc/wpa_supplicant.conf -t &
```

### 3. Obtain IP Address

```shell
udhcpc -i wlan0
```

### 4. Test the Network

```shell
root@imx8mp-debix:/lib/firmware/brcm# ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=2 ttl=113 time=20.7 ms  
64 bytes from 8.8.8.8: icmp_seq=3 ttl=113 time=18.8 ms  
64 bytes from 8.8.8.8: icmp_seq=4 ttl=113 time=18.6 ms  
```