# 📘 README — DEBIX (i.MX8MP) 2-Wire UART

This directory contains Device Tree Overlay files for enabling **2-wire UART (TX/RX)** functionality on the **i.MX8MP SoC with the DEBIX development board**.

---

📂 **File List (2-Wire UART)**

| UART Device | DTSO File Name                     | Pin Mapping Description |
| ----------- | ---------------------------------- | ----------------------- |
| UART2       | `imx8mp-debix-pin9_11-UART2.dtso`  | `UART2_RXD / UART2_TXD` |
| UART3       | `imx8mp-debix-pin13_15-UART3.dtso` | `UART3_RXD / UART3_TXD` |
| UART4       | `imx8mp-debix-pin17_19-UART4.dtso` | `UART4_RXD / UART4_TXD` |

---

📌 **Check Device Node**

Verify whether the corresponding serial device files are generated:

```shell
ls /dev/ttymxc*
```

---

🧪 **Testing Method (using `minicom`)**

Take `ttymxc2` as an example. Connect the TX/RX lines to another device to perform UART testing:

```shell
sudo minicom -D /dev/ttymxc2
```
