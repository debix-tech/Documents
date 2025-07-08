# CAN 配置说明 - i.MX8MP



## 📂 设备树文件

| CAN 控制器 | DTSO 文件名                       | 引脚名称              |
| ---------- | --------------------------------- | --------------------- |
| CAN1       | `imx8mp-debix-pin31_33-CAN1.dtso` | `SAI5_RXD2/SAI5_RXD1` |
|            | `imx8mp-debix-pin34_36-CAN1.dtso` | `SPDIF_RX_/SPDIF_TX`  |
| CAN2       | `imx8mp-debix-pin13_15-CAN2.dtso` | `UART3_RXD/UART3_TXD` |
|            | `imx8mp-debix-pin35_37-CAN2.dtso` | `SAI5_MCLK/SAI5_RXD3` |



测试：

1.硬件连接：

把两个串口连接在一起，比如CAN1和CAN2：

然后执行

```shell
root@imx8mp-debix:/sys/class/thermal/thermal_zone1# ip link set can0 up type can bitrate 1000000 dbitrate 5000000 fd on
[11072.340539] IPv6: ADDRCONF(NETDEV_CHANGE): can0: link becomes ready
root@imx8mp-debix:/sys/class/thermal/thermal_zone1# ip link set can1 up type can bitrate 1000000 dbitrate 5000000 fd on
[11073.718111] IPv6: ADDRCONF(NETDEV_CHANGE): can1: link becomes ready

```

2.发送数据，CAN 收发测试

在终端1运行监听工具

```shell
candump -ta can1
```

在终端2运行发送数据

```shell
cangen can0
```

