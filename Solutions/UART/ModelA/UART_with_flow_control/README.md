## 📘 README — DEBIX (i.MX8MP) 4-Wire UART

This directory contains Device Tree Overlay files for enabling **4-wire UART (TXD/RXD/RTS/CTS)** on the **DEBIX Model A / i.MX8MP platform**.

---

## 📂 File List (4-Wire UART)

| UART Device | DTSO File Name                           | Pin Mapping Description                                |
| ----------- | ---------------------------------------- | ------------------------------------------------------ |
| UART2       | `imx8mp-debix-pin17_19-UART2.dtso`       | `UART2_TXD / UART2_RXD / UART4_RXD / UART4_TXD`        |
| UART3       | `imx8mp-debix-pin14_16_18_20-UART3.dtso` | `ECSPI1_MOSI / ECSPI1_SCLK / ECSPI1_SS0 / ECSPI1_MISO` |
| UART4       | `imx8mp-debix-pin22_24_26_28-UART4.dtso` | `ECSPI2_MOSI / ECSPI2_SCLK / ECSPI2_SS0 / ECSPI2_MISO` |

---

📌 **Check Device Node**

Verify whether the corresponding serial device files are generated:

```shell
ls /dev/ttymxc*
```

---

🧪 **Testing Method (using `minicom`)**

Take `ttymxc2` as an example. Connect the TX/RX/RTS/CTS lines to another device to perform UART testing.

```shell
sudo minicom -D /dev/ttymxc2
```
