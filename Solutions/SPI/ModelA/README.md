## 📘 README — DEBIX (i.MX8MP) SPI Interface

This directory contains Device Tree Overlay (`.dtso`) files to enable **SPI buses** on the **i.MX8M Plus SoC**, which can be used to connect SPI devices.

---

## 📂 List of Device Tree Overlays

| SPI Controller | DTSO Filename                           | Pin Names                                                   |
| -------------- | --------------------------------------- | ----------------------------------------------------------- |
| SPI1       | `imx8mp-debix-pin14_16_18_20-SPI1.dtso` | `ECSPI1_SCLK / ECSPI1_MOSI / ECSPI1_MISO / CS(GPIO5_IO09)` |
| SPI2       | `imx8mp-debix-pin22_24_26_28-SPI2.dtso` | `ECSPI2_SCLK / ECSPI2_MOSI / ECSPI2_MISO / CS(GPIO5_IO13)` |

---

### 🔍 Check for Device Node

```shell
ls /dev/spidev*
```

---

## 🔄 Loopback Test

> Connect **MOSI** and **MISO** pins together to perform a loopback test.

Example Device Tree configuration:

```dts
&ecspi1 {
    #address-cells = <1>;
    #size-cells = <0>;
    fsl,spi-num-chipselects = <1>;
    pinctrl-names = "default";
    pinctrl-0 = <&pinctrl_ecspi1 &pinctrl_ecspi1_cs>;
    cs-gpios = <&gpio5 9 GPIO_ACTIVE_LOW>;
    status = "okay";

    spidev1: spi@0 {
        reg = <0>;
        compatible = "rohm,dh2228fv";
        spi-max-frequency = <20000000>;
    };
};
```

---

### 🧪 Run Loopback Test

```shell
root@imx8mp-debix:~# spidev_test -D /dev/spidev1.0 -v -p "12345678"
spi mode: 0x0
bits per word: 8
max speed: 500000 Hz (500 kHz)
TX | 31 32 33 34 35 36 37 38 __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __  |12345678|
RX | FF FF FF FF FF FF FF FF __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __  |........|
```

If MOSI and MISO are properly connected, the `RX` output will display `12345678`.
