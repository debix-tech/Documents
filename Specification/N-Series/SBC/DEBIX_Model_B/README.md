# DEBIX Model B Industrial Single Board Computer

<p align="center">
<img  width=70% height=auto src="./DEBIX_Model_B_1.png" alt="DEBIX Model B(1)">
</p>

## Overview
DEBIX Model B is a high-performance, industrial-grade single-board computer designed 
for challenging and demanding applications. It boasts superior features compared to 
its predecessor, DEBIX Model A, making it a compelling choice for projects operating in 
extreme temperature conditions.

## Main Features
- **Wider Operating Temp.**  
  DEBIX Model B confidently operates in -40°C to 85°C environment. This enhanced resilience makes it ideal for industrial applications with extreme temperatures.
- **Shared DNA with DEBIX Model A**  
  Both share the same powerful i.MX 8M Plus CPU with 2.3 TOPS NPU and identical PCB design, contributing to their similar appearance. They also offer the same type and number of interfaces.
- **Targeted Upgrade**  
  Upgrade individual chips and components on the board, it is convenient for customers to choose a board according to the temperatures of their real-world application environment.
- **Powerful Connectivity**  
  A full suite of connectivity options, including Gigabit network, 2.4GHz & 5GHz Wi-Fi, Bluetooth 5.0, high-speed USB 3.0, and PCIe support.
- **Advanced Multimedia**  
  Multimedia capabilities are equally impressive, featuring1080p60 video encode and decode (including H.265 and H.264), 3D/2D graphic acceleration, and advanced audio and voice functionalities.
- **Software Compatibility**
  Support Android 11, Yocto-L6.6.36, Ubuntu 22.04, Debian 12 and Windows10 IoT Enterprise operating systems.

<p align="center">
<img  width=60% height=auto src="./DEBIX_Model_B_2.png" alt="DEBIX Model B(2)">
</p>

## Specification
| System          |                                                                         |
|-----------------|-------------------------------------------------------------------------|
| CPU             | NXP i.MX 8M Plus (default), 4 x ARM Cortex-A53, comes with an integrated neural processing unit (NPU) that delivers up to 2.3 TOPS. Industrial grade CPU runs at 1.6GHz.<br>(i.MX 8M Plus series CPU optional) |
| Memory          | 4GB LPDDR4 (1GB/2GB optional)                                         |
| Storage         | 16GB eMMC (8GB/32GB/64GB/128GB/256GB optional), support Micro SD card |
| OS              | Android 11, Yocto-L6.6.36, Ubuntu 22.04, Debian 12, Win10 IoT Enterprise (also supports OpenWRT and FreeRTOS)<br>*Note: 4GB RAM required for Win10 IoT Enterprise*                  |
|**I/O Interface**|                                                                      
| Gigabit Ethernet| 1 x Gigabit Ethernet, supports TSN and POE power supply (need POE power device module)<br>1 x Gigabit Ethernet via 12pin header (without network transformer)              |
| WiFi & BT       | 2.4GHz & 5GHz Wi-Fi5, Bluetooth 5.0                                     |
| USB             | 4 x USB 3.0 Host, 1 x USB 2.0 OTG                                       |
| Audio           | 1 x Headphone and Mic combo port                                        |
| HDMI           | 1 x HDMI OUT                                                            |
|**Expansion**    |
| 40-Pin Dual-Row Header | (1) 3 x UART, 2 x I2C, 2 x SPI, 2 x CAN, 6 x GPIO for default, can be reused as I2S, PWM, SPDIF and GPIO through software configuration<br>(2) 5V power supply, system reset, ON/OFF |
| LVDS            | 1 x LVDS, single/dual channel 8bit                                      |
| MIPI CSI        | 1 x MIPI CSI (4-lane)                                                   |
| MIPI DSI        | 1 x MIPI DSI (4-lane)                                                   |
| PCIe            | 1 x PCIe Gen3 (1-lane)                                                  |
|**Power Supply**|
| Power Supply    | DC 5V/3A via Type-C                                                     |
|**Mechanical & Environmental**|
| Size            | 85.0mm × 56.0mm (±0.5mm)                                                |
| Operating Temp. | -40°C to 85°C                                                           |
| Net Weight      | 46g (±0.5g)                                                             |
| Net Weight      | 72g (±0.5g)                                                             |

## Product Version
| Version | CPU | NPU | VPU | ISP | HiFi4 |
|-------- |-----|-----|-----|-----|-------|
| DEBIX Model B Standard | NXP i.MX 8M Plus | 1 | 1 | 1 | 1 |
| DEBIX Model B Lite | NXP i.MX 8M Plus Quad Lite | N/A | N/A | N/A | N/A |

## Certificates:
<img src="./Certificates.png" alt="Certificates" width=70% height=auto>

## I/O Interfaces:
<p align="center">
<img src="./Interface_1.png" alt="Interface(1)" width=90% height=auto>
<img src="./Interface_2.png" alt="Interface(2)" width=90% height=auto>
</p>

## Ordering Codes
| RAM LPDDR4  | eMMC Storage | PN for Model B | PN for Model B Lite |
|-------------|--------------|----------------|---------------------|
| **1GB DDR** | 8GB   | Model B-D1E8    | Model B Lite-D1E8 |
|       | 16GB  | Model B-D1E16   | Model B Lite-D1E16 |
|       | 32GB  | Model B-D1E32   | Model B Lite-D1E32 |
|       | 64GB  | Model B-D1E64   | Model B Lite-D1E64 |
| **2GB DDR** | 8GB   | Model B-D2E8    | Model B Lite-D2E8 |
|       | 16GB  | Model B-D2E16   | Model B Lite-D2E16 |
|       | 32GB  | Model B-D2E32   | Model B Lite-D2E32 |
|       | 64GB  | Model B-D2E64   | Model B Lite-D2E64 |
| **4GB DDR** | 8GB   | Model B-D4E8    | Model B Lite-D4E8 |
|       | 16GB  | Model B-D4E16   | Model B Lite-D4E16 |
|       | 32GB  | Model B-D4E32   | Model B Lite-D4E32 |
|       | 64GB  | Model B-D4E64   | Model B Lite-D4E64 |

## Compatible with DEBIX's Accessories
| Product                     | Model               |
|-----------------------------|---------------------|
| DEBIX Fanless Aluminum Enclosure | EMC-7090B Model A/B|
| I/O Board                  | EMB-AS-E01         |
| 4G Board                   | EMB-AS-05          |
| LoRa Board                 | EMB-AS-03          |
| SBC POE Board              | EMB-AS-06          |
| DEBIX Camera Modules       | Camera 200A; Camera 500A; Camera 1300A    |
| DEBIX Display Screens      | DEBIX TD050A; DEBIX TD070A; DEBIX TD101A; DEBIX TD050H; DEBIX TD070H; DEBIX TD101H |

## Safety Instructions and Warnings:
**General:**
- Avoid exposure to water, moisture and conductive surfaces while operating.
- Handle with care to avoid mechanical or electrical damage to the circuit board and connectors.
- Only handle the board by the edges when powered on to minimize the risk of electrostatic discharge damage.

**Power:**
- Use only a 5V/3A DC minimum external power supply that complies with relevant regulations and standards for your country.

**Environment:**
- Operate in a well-ventilated environment, even if using a case.
- Place on a stable, flat, non-conductive surface and avoid contact with conductive items.

**Connections:**
- Only connect compatible devices to the GPIO ports to avoid damage and warranty
voiding.
- Use peripherals that comply with relevant standards for the country of use and ensure proper insulation and operation.

**Additional notes:**
- This summary is not exhaustive, please refer to the full User Manual for details.
- If you are unsure about any aspect of safety or operation, consult a qualified
professional.

## Contact Us
- **Headquarters**: DEBIX Technology Inc., 8345 Gold River Ct., Las Vegas, NV 89113, USA  
- **Factory**: 5-6/F., East Zone, Shunheda A2 Building, Liqxiandong Industrial Park, XiLi, Nanshan Dist., Shenzhen, China  <img src="../../../Discord_QRcode.png" alt="Discord(QRcode)" width=15% height=auto align="right">
- **Email**: info@debix.io  
- **Website**: [www.debix.io](https://www.debix.io)  
- **Community**: [Discord](https://discord.com/invite/adaHHaDkH2)
 