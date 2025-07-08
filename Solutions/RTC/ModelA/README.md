## 🕒 RTC 使用说明文档 – i.MX8MP 平台



## 📋 简介

平台支持 **两个 RTC 设备**：

| RTC名称    | 类型    | 接口        | 设备树节点       | 描述                             |
| ---------- | ------- | ----------- | ---------------- | -------------------------------- |
| `hym8563`  | 外部RTC | I2C4 @ 0x51 | `&i2c4/hym8563`  | 独立电池供电、精度高、可中断唤醒 |
| `snvs_rtc` | 内部RTC | SNVS模块    | `&snvs/snvs_rtc` | 芯片自带低功耗RTC，备用方案      |



📂 设备树配置说明

```shell
	hym8563: hym8563@51 {
		compatible = "haoyu,hym8563";
		reg = <0x51>;
		#clock-cells = <0>;
		clock-frequency = <32768>;
		clock-output-names = "xin32k";
		init_date="2022/04/12";
		interrupt-parent = <&gpio2>;
		interrupts = <11 IRQ_TYPE_EDGE_FALLING>;
		
		pinctrl-names = "default";
		pinctrl-0 = <&pinctrl_rtc_int>;
	};

```

* 挂载在 `i2c4` 总线地址 `0x51`

* 支持中断唤醒

* 使用 `xin32k` 作为输出名称



🔧 驱动位置

`hym8563` 驱动：`drivers/rtc/rtc-hym8563.c`

`snvs_rtc` 驱动：`drivers/rtc/rtc-snvs.c`



🧪 使用方法

**a.测试读写时间**

1.查看设备

```shell
root@imx8mp-debix:/sys/class/rtc# ls
rtc0  rtc1
```

2.设置时间

```shell
hwclock -w -f /dev/rtc0    # 将系统时间写入RTC
```

3.读取时间

```shell
hwclock -r -f /dev/rtc0
```



**b.测试RTC中断功能：**

1.设置一分钟后闹钟(hym8563只能设置以分钟为最小单位的闹钟)

```shell
root@imx8mp-debix:~# hwclock --systohc -f /dev/rtc1
root@imx8mp-debix:~# hwclock --hctosys -f /dev/rtc1 
root@imx8mp-debix:~# rtcwake -m no -d /dev/rtc0 -t $(date +%s -d '+1 minute') 
rtcwake: wakeup using /dev/rtc0 at Thu Apr  6 00:07:28 2023
root@imx8mp-debix:~# cat /proc/interrupts |grep hym8563
149:          0          0          0          0  gpio-mxc   3 Level     hym8563
```



2.查看中断

```

root@imx8mp-debix:~# cat /proc/interrupts |grep hym8563
149:          1          0          0          0  gpio-mxc   3 Level     hym8563

```

当时间到了之后，中断次数会加一





**c.测试RTC唤醒功能**

```shell
root@imx8mp-debix:~# hwclock --systohc -f /dev/rtc0
root@imx8mp-debix:~# hwclock -rf /dev/rtc0
2023-04-06 00:12:32.852331+00:00
root@imx8mp-debix:~# date
Thu Apr  6 00:12:36 UTC 2023
root@imx8mp-debix:~# rtcwake -s 60 -m mem -d /dev/rtc0
rtcwake: wakeup from "mem" using /dev/rtc0 at Thu Apr  6 00:13:48 2023
[  770.138344] PM: suspend entry (deep)
[  770.142180] Filesystems sync: 0.000 seconds
[  770.147816] Freezing user space processes
[  770.153491] Freezing user space processes completed (elapsed 0.001 seconds)
[  770.160484] OOM killer disabled.
[  770.163710] Freezing remaining freezable tasks
[  770.169404] Freezing remaining freezable tasks completed (elapsed 0.001 seconds)
[  770.176821] printk: Suspending console(s) (use no_console_suspend to debug)
[  770.404580] imx-dwmac 30bf0000.ethernet ens33: FPE workqueue stop
[  770.404641] fec 30be0000.ethernet ens34: Link is Down
[  770.544106] PM: suspend devices took 0.364 seconds
[  770.564107] Disabling non-boot CPUs ...
[  770.564592] IRQ238: set affinity failed(-22).
[  770.565635] psci: CPU1 killed (polled 0 ms)
[  770.566816] IRQ238: set affinity failed(-22).
[  770.567864] psci: CPU2 killed (polled 0 ms)
[  770.568589] IRQ238: set affinity failed(-22).
[  770.568635] psci: CPU3 killed (polled 0 ms)
[  770.569452] Enabling non-boot CPUs ...
[  770.569861] Detected VIPT I-cache on CPU1
[  770.569912] GICv3: CPU1: found redistributor 1 region 0:0x00000000388a0000
[  770.569947] CPU1: Booted secondary processor 0x0000000001 [0x410fd034]
[  770.571722] CPU1 is up
[  770.572074] Detected VIPT I-cache on CPU2
[  770.572108] GICv3: CPU2: found redistributor 2 region 0:0x00000000388c0000
[  770.572130] CPU2: Booted secondary processor 0x0000000002 [0x410fd034]
[  770.572434] CPU2 is up
[  770.572768] Detected VIPT I-cache on CPU3
[  770.572797] GICv3: CPU3: found redistributor 3 region 0:0x00000000388e0000
[  770.572815] CPU3: Booted secondary processor 0x0000000003 [0x410fd034]
[  770.573110] CPU3 is up
[  770.892024] imx-dwmac 30bf0000.ethernet ens33: configuring for phy/rgmii-id link mode
[  770.930153] imx-dwmac 30bf0000.ethernet ens33: No Safety Features support found
[  770.930173] imx-dwmac 30bf0000.ethernet ens33: IEEE 1588-2008 Advanced Timestamp supported
[  770.930327] imx-dwmac 30bf0000.ethernet ens33: FPE workqueue start
[  770.930478] xhci-hcd xhci-hcd.1.auto: xHC error in resume, USBSTS 0x401, Reinit
[  770.930487] usb usb1: root hub lost power or was reset
[  770.930492] usb usb2: root hub lost power or was reset
[  770.930507] xhci-hcd xhci-hcd.2.auto: xHC error in resume, USBSTS 0x401, Reinit
[  770.930514] usb usb3: root hub lost power or was reset
[  770.930518] usb usb4: root hub lost power or was reset
[  770.930710] caam 30900000.crypto: registering rng-caam
[  771.087345] brcmfmac: brcmf_fw_alloc_request: using brcm/brcmfmac43455-sdio for chip BCM4345/6
[  771.087413] brcmfmac mmc0:0001:1: Direct firmware load for brcm/brcmfmac43455-sdio.fsl,imx8mp-evk.bin failed with error -2
[  771.087421] brcmfmac mmc0:0001:1: Falling back to sysfs fallback for: brcm/brcmfmac43455-sdio.fsl,imx8mp-evk.bin
[  771.224175] usb 3-1: reset high-speed USB device number 2 using xhci-hcd
[  771.752087] usb 3-1.4: reset high-speed USB device number 3 using xhci-hcd
[  773.972568] fec 30be0000.ethernet ens34: Link is Up - 1Gbps/Full - flow control rx/tx
[  774.160172] usb 4-1: reset SuperSpeed USB device number 2 using xhci-hcd
[  774.305893] PM: resume devices took 3.728 seconds
[  774.547174] OOM killer enabled.
[  774.550318] Restarting tasks ... done.
[  774.558363] random: crng reseeded on system resumption
[  774.563926] PM: suspend exit

```

