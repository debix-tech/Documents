# 🌡️ Thermal Zone Usage Guide – i.MX8MP Platform

## 📋 Overview

The system defines two thermal zones:

| Zone Name     | Sensor Source | Description                                                         |
| ------------- | ------------- | ------------------------------------------------------------------- |
| `cpu-thermal` | `tmu 0`       | Monitors CPU core temperature and handles dynamic frequency scaling |
| `soc-thermal` | `tmu 1`       | Monitors overall SoC temperature for system protection              |
---
Each zone includes two trip points:
* **Passive Mode**: When temperature exceeds the set value, the system throttles CPU performance to reduce heat.
* **Critical Mode**: When temperature becomes too high, the system triggers a shutdown for protection.


## 🧪 How to Use

### 1️⃣ Check Current Temperature

```bash
root@imx8mp-debix:~# cat /sys/class/thermal/thermal_zone0/temp
55000
root@imx8mp-debix:~# cat /sys/class/thermal/thermal_zone1/temp
54000
```

### 2️⃣ Check Cooling Device Status

```bash
root@imx8mp-debix:~# cat /sys/class/thermal/cooling_device*/cur_state
0
0
0
```

This indicates that **all cooling devices (e.g., CPU frequency scalers)** are currently inactive, meaning system temperatures are within the normal range and no thermal throttling is being applied.

### 3️⃣ Check Trip Point Settings

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

### 🔧 Current Trip Point Configuration (unit: millidegree Celsius, i.e., °C × 1000):

| Thermal Zone    | trip\_point\_0\_temp | trip\_point\_1\_temp |
| --------------- | -------------------- | -------------------- |
| `thermal_zone0` | 95000 → 95°C         | 105000 → 105°C       |
| `thermal_zone1` | 95000 → 95°C         | 105000 → 105°C       |

### 🧩 Notes

* `trip_point_0_temp = 95000`: This is the **passive thermal point**. Exceeding this temperature will trigger cooling actions like frequency throttling.
* `trip_point_1_temp = 105000`: This is the **critical thermal point**. Exceeding this value may trigger system shutdown or kernel panic for hardware protection.

These values can be modified in the device tree under the `thermal-zones` node using the `temperature` property, or updated at runtime via terminal:

```bash
root@imx8mp-debix:~# cat /sys/class/thermal/thermal_zone0/trip_point_1_temp 
105000
root@imx8mp-debix:~# echo 100000 > /sys/class/thermal/thermal_zone0/trip_point_1_temp 
root@imx8mp-debix:~# cat /sys/class/thermal/thermal_zone0/trip_point_1_temp 
100000
```

---

### 4️⃣ Simulate Overheating – Trigger System Shutdown

```bash
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
