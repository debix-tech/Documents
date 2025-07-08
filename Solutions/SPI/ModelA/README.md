## 📘 README — DEBIX (i.MX8MP) SPI 接口

本目录包含启用 **i.MX8M Plus SoC** 上 SPI 总线的设备树覆盖文件（`.dtso`），可用于连接 SPI



## 📂 设备树覆盖文件一览

| SPI 控制器 | DTSO 文件名                             | 引脚名称                                                   |
| ---------- | --------------------------------------- | ---------------------------------------------------------- |
| SPI1       | `imx8mp-debix-pin14_16_18_20-SPI1.dtso` | `ECSPI1_SCLK / ECSPI1_MOSI / ECSPI1_MISO / CS(GPIO5_IO09)` |
| SPI2       | `imx8mp-debix-pin22_24_26_28-SPI2.dtso` | `ECSPI2_SCLK / ECSPI2_MOSI / ECSPI2_MISO / CS(GPIO5_IO13)` |





查看设备文件

```shell
ls /dev/spidev*
```



回环测试：

需要把MOSI和MISO连接在一起。

设备树配置如下：

```shell
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



🧪 进行回环测试

```shell
root@imx8mp-debix:~# spidev_test -D /dev/spidev1.0 -v -p "12345678"
spi mode: 0x0
bits per word: 8
max speed: 500000 Hz (500 kHz)
TX | 31 32 33 34 35 36 37 38 __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __  |12345678|
RX | FF FF FF FF FF FF FF FF __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __ __  |........|

```

如果连接在一起的话`RX`就会看到`12345678`
