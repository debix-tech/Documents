# CAN Configuration Guide - i.MX8MP

## 📂 Device Tree Files

| CAN Controller | DTSO File Name                    | Pin Names             |
| -------------- | --------------------------------- | --------------------- |
| CAN1           | `imx8mp-debix-pin31_33-CAN1.dtso` | `SAI5_RXD2/SAI5_RXD1` |
|                | `imx8mp-debix-pin34_36-CAN1.dtso` | `SPDIF_RX_/SPDIF_TX`  |
| CAN2           | `imx8mp-debix-pin13_15-CAN2.dtso` | `UART3_RXD/UART3_TXD` |
|                | `imx8mp-debix-pin35_37-CAN2.dtso` | `SAI5_MCLK/SAI5_RXD3` |

---

### 🔧 Test Procedure:

#### 1. Hardware Connection:

Connect the two CAN interfaces together (e.g., **CAN1 and CAN2**), then run the following commands:

```shell
root@imx8mp-debix:/sys/class/thermal/thermal_zone1# ip link set can0 up type can bitrate 1000000 dbitrate 5000000 fd on
[11072.340539] IPv6: ADDRCONF(NETDEV_CHANGE): can0: link becomes ready

root@imx8mp-debix:/sys/class/thermal/thermal_zone1# ip link set can1 up type can bitrate 1000000 dbitrate 5000000 fd on
[11073.718111] IPv6: ADDRCONF(NETDEV_CHANGE): can1: link becomes ready
```

---

#### 2. Data Transmission Test (CAN Send/Receive)

**In Terminal 1**, run the CAN listener:

```shell
candump -ta can1
```

**In Terminal 2**, send test data:

```shell
cangen can0
```
