# 🌡️ Thermal Zone 使用说明 – i.MX8MP 平台

## 📋 简介

该系统定义了两个热感区域（thermal zones）：

| 区域名称      | 传感器来源 | 用途说明                   |
| ------------- | ---------- | -------------------------- |
| `cpu-thermal` | `tmu 0`    | CPU 核心温度监测与动态调频 |
| `soc-thermal` | `tmu 1`    | SoC 整体温度监测与系统保护 |

每个区域包含两个温度触发点（trip point）：

- **被动模式（passive）**：当温度超过设定值时，限制 CPU 性能以降低温度；
- **临界模式（critical）**：当温度极高时触发关机保护。





🧪 使用方法

1️⃣ 查看当前温度

```shell
root@imx8mp-debix:~# cat /sys/class/thermal/thermal_zone0/temp
55000
root@imx8mp-debix:~# cat /sys/class/thermal/thermal_zone1/temp
54000
```

2️⃣ 查看 cooling device 状态

```shell
root@imx8mp-debix:~# cat /sys/class/thermal/cooling_device*/cur_state
0
0
0

```

这意味着目前**所有 cooling device（散热设备，如 CPU 调频器）都未处于激活状态**，即系统温度处于正常范围内，没有触发降温策略。

3️⃣ 查看触发的trip

```
root@imx8mp-debix:~# cat /sys/class/thermal/thermal_zone0/trip_point_1_temp
105000
root@imx8mp-debix:~# cat /sys/class/thermal/thermal_zone0/trip_point_0_temp
95000
root@imx8mp-debix:~# cat /sys/class/thermal/thermal_zone1/trip_point_1_temp
105000
root@imx8mp-debix:~# cat /sys/class/thermal/thermal_zone1/trip_point_0_temp
95000

```

### 🔧 当前 trip point 配置（单位：毫摄氏度，°C × 1000）：

| Thermal Zone    | trip_point_0_temp | trip_point_1_temp |
| --------------- | ----------------- | ----------------- |
| `thermal_zone0` | 95000 → 95°C      | 105000 → 105°C    |
| `thermal_zone1` | 95000 → 95°C      | 105000 → 105°C    |

### 🧩 说明

- `trip_point_0_temp = 95000`：这是 **被动温控点**，超过这个温度将触发降频等 cooling 动作；
- `trip_point_1_temp = 105000`：这是 **临界温控点**，超过此温度系统可能会触发关机或内核 panic 保护；



修改以上的值可以通过设备树中的`thermal-zones`节点的`temperature`属性来修改，或者通过终端修改，如下：

```shell
root@imx8mp-debix:~# cat  /sys/class/thermal/thermal_zone0/trip_point_1_temp 
105000
root@imx8mp-debix:~# echo 100000 >  /sys/class/thermal/thermal_zone0/trip_point_1_temp 
root@imx8mp-debix:~# cat  /sys/class/thermal/thermal_zone0/trip_point_1_temp 
100000

```





4.模拟高温触发--系统进入关机

```shell
root@imx8mp-debix:~# echo 105000 > /sys/class/thermal/thermal_zone0/emul_temp 
[ 2396.221023] System is too hot. GPU3D will work at 1/64 clock.
[ 2396.227218] thermal thermal_zone0: cpu-thermal: critical temperature reached, shutting down
[ 2396.235599] reboot: HARDWARE PROTECTION shutdown (Temperature too high)

Message from syslogd@imx8mp-debix at Thu Apr  6 00:41:15 2023 ...
kernel: thermal thermal_zone0: cpu-thermal: critical temperature reached, shutting down

Message from syslogd@imx8mp-debix at Thu Apr  6 00:41:15 2023 ...
kernel: reboot: HARDWARE PROTECTION shutdown (Temperature too high)
root@imx8mp-debix:~#          Stopping Sess񞟏K  ] Removed slice Slice /system/modprobe.
.....
.....
         Stopping Linux Firmware Loader Daemon...
         Stopping Getty on tty1...
         Stopping NFS status monitor for NFSv2/3 locking....
         Stopping Telephony service...
         Stopping LSB: Run /etc/rc.local if it exist...
         Stopping Serial Getty on ttymxc1...
         Stopping System Logging Service...
[ 2396.812755] thermal thermal_zone0: cpu-thermal: critical temperature reached, shutting down
[ 2396.821145] reboot: HARDWARE PROTECTION shutdown (Temperature too high)
         Stopping Load/Save OS Random Seed...
         Stopping Weston, a Wayland…ositor, as a system service...

```

