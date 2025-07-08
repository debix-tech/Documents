# 📘 README — DEBIX (i.MX8MP) 两线串口

本目录下包含用于启用 **i.MX8MP SoC 在 DEBIX 开发板**上 **两线 UART（TX/RX）串口功能** 的设备树

📂 文件列表（两线 UART）

| 串口设备 | DTSO 文件名                        | 引脚映射名称            |
| -------- | ---------------------------------- | ----------------------- |
| UART2    | `imx8mp-debix-pin9_11-UART2.dtso`  | `UART2_RXD / UART2_TXD` |
| UART3    | `imx8mp-debix-pin13_15-UART3.dtso` | `UART3_RXD / UART3_TXD` |
| UART4    | `imx8mp-debix-pin17_19-UART4.dtso` | `UART4_RXD / UART4_TXD` |



📌 查看

查看是否生成对应的串口设备文件：

```shell
ls /dev/ttymxc*
```



🧪 测试方法（使用 `minicom`）

以ttymxc2为例，连接 TX/RX 至另一台设备即可进行串口测试。

```
sudo minicom -D /dev/ttymxc2
```

