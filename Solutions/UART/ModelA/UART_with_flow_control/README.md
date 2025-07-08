## 📘 README — DEBIX (i.MX8MP) 四线串口

本目录下包含用于在 **DEBIX Model A / i.MX8MP 平台**上启用 **四线 UART（TXD/RXD/RTS/CTS）**



## 📂 文件列表（四线 UART）

| 串口设备 | DTSO 文件名                              | 引脚映射名称                                           |
| -------- | ---------------------------------------- | ------------------------------------------------------ |
| UART2    | `imx8mp-debix-pin17_19-UART2.dtso`       | `UART2_TXD / UART2_RXD / UART4_RXD / UART4_TXD`        |
| UART3    | `imx8mp-debix-pin14_16_18_20-UART3.dtso` | `ECSPI1_MOSI / ECSPI1_SCLK / ECSPI1_SS0 / ECSPI1_MISO` |
| UART4    | `imx8mp-debix-pin22_24_26_28-UART4.dtso` | `ECSPI2_MOSI / ECSPI2_SCLK / ECSPI2_SS0 / ECSPI2_MISO` |

📌 查看

查看是否生成对应的串口设备文件：

```shell
ls /dev/ttymxc*
```



🧪 测试方法（使用 `minicom`）

以ttymxc2为例，连接 TX/RX/RTS/CTS 测试至另一台设备即可进行串口测试。

```
sudo minicom -D /dev/ttymxc2
```

