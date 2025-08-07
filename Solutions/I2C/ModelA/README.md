## 📘 README — DEBIX (i.MX8MP) I²C

This directory contains Device Tree Overlay files (`.dtso`) for enabling I²C buses on the **i.MX8M Plus SoC**, which can be used to connect I²C devices.

## 📂 List of Device Tree Files

| I²C Controller | DTSO File Name                    | Pin Names               |
| -------------- | --------------------------------- | ----------------------- |
| I²C4           | `imx8mp-debix-pin21_23-I2C4.dtso` | `I2C4_SCL/I2C4_SDA`   |
| I²C5           | `imx8mp-debix-pin34_36-I2C5.dtso` | `SPDIF_TX/SPDIF_RX`   |
| I²C5           | `imx8mp-debix-pin37_38-I2C5.dtso` | `SAI5_RXD0/SAI5_MCLK` |
| I²C6           | `imx8mp-debix-pin17_19-I2C6.dtso` | `UART4_RXD/UART4_TXD` |
| I²C6           | `imx8mp-debix-pin25_27-I2C6.dtso` | `SAI5_RXFS/SAI5_RXC`  |

---

### 🧪 Testing Method

#### 1️⃣ Check available I²C buses:

```shell
root@imx8mp-debix:/sys/class/pwm/pwmchip0/pwm0# ls /dev/i2c-*
/dev/i2c-0  /dev/i2c-1  /dev/i2c-2  /dev/i2c-3  /dev/i2c-5  /dev/i2c-6
```

#### 2️⃣ List I²C adapters using `i2cdetect`:

```shell
root@imx8mp-debix:/sys/class/pwm/pwmchip0/pwm0# i2cdetect -l
i2c-0	i2c       	30a20000.i2c                    	I2C adapter
i2c-1	i2c       	30a30000.i2c                    	I2C adapter
i2c-2	i2c       	30a40000.i2c                    	I2C adapter
i2c-3	i2c       	30a50000.i2c                    	I2C adapter
i2c-5	i2c       	30ae0000.i2c                    	I2C adapter
i2c-6	i2c       	DesignWare HDMI                 	I2C adapter
```

#### 3️⃣ Scan for connected I²C devices:

```shell
root@imx8mp-debix:/sys/class/thermal/thermal_zone1# i2cdetect -y 3
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:                         -- -- -- -- -- -- -- -- 
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
20: UU -- -- UU -- -- -- -- -- -- -- -- -- -- -- -- 
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
40: -- -- -- -- -- -- -- -- UU -- -- -- -- -- -- -- 
50: -- UU UU -- -- -- -- -- -- -- -- -- -- -- -- -- 
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
70: -- -- -- -- -- -- -- --  
```

> Note: `UU` indicates the address is already in use by a driver.
