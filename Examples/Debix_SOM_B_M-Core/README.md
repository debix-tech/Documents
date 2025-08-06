## 📶 Debugging and Development of the M33 Core on DEBIX SOMB  

Two approaches for engineering debugging and development of the M33 core:  

The first method uses the board's built-in firmware for development.  
The second method leverages IAR Embedded Workbench to build portable FreeRTOS files for development.  

---

### ✅ A. On-board Firmware Debugging (Method 1)  

📦 1. **Load Official M33 Firmware**  
The `/lib/firmware/` directory contains 5 M-core firmware files for direct validation:  
```shell
echo /lib/firmware/imx93-11x11-evk_m33_TCM_rpmsg_lite_str_echo_rtos.elf > /sys/class/remoteproc/remoteproc0/firmware
```

🚀 2. **Start M33 Core Processor**  
```shell
root@DebixSomB:/sys/class/remoteproc/remoteproc0# echo start > state
...
[68352.323252] remoteproc remoteproc0: remote processor imx-rproc is now up
```

🔌 3. **Load RPMsg Communication Driver**  
Character transmission requires driver installation:  
```shell
modprobe imx_rpmsg_tty
```  
This creates `/dev/ttyRPMSG30` in the dev directory.  

💬 4. **Send Data from A-core to M33 Core**  
```shell
echo 1234 > /dev/ttyRPMSG30
```

---

### ⚠️ Critical Note: Avoid UART Conflicts  
If **M33 uses UART2**, disable the corresponding UART in the A-core device tree to prevent conflicts:  
```c
diff --git a/arch/arm64/boot/dts/freescale/imx93-debix-SOMB.dts b/arch/arm64/boot/dts/freescale/imx93-debix-SOMB.dts
index 903e06e75..a9cc27659 100755
--- a/arch/arm64/boot/dts/freescale/imx93-debix-SOMB.dts
+++ b/arch/arm64/boot/dts/freescale/imx93-debix-SOMB.dts
@@ -936,11 +936,11 @@ &lpuart1 { /* console */
 };
 
 //Add J36
-&lpuart2 {
-       pinctrl-names = "default";
-       pinctrl-0 = <&pinctrl_uart2>;
-       status = "okay";
-};
+// &lpuart2 {
+//     pinctrl-names = "default";
+//     pinctrl-0 = <&pinctrl_uart2>;
+//     status = "okay";
+// };
 
 //BT
 &lpuart5 {
@@ -1203,12 +1203,12 @@ MX93_PAD_CCM_CLKO3__GPIO4_IO28  0x31e
 
 
 //Add J36 UART
-       pinctrl_uart2: uart2grp {
-               fsl,pins = <
-                       MX93_PAD_UART2_RXD__LPUART2_RX             0x31e
-                       MX93_PAD_UART2_TXD__LPUART2_TX             0x31e
-               >;
-       };
+       // pinctrl_uart2: uart2grp {
+       //      fsl,pins = <
+       //              MX93_PAD_UART2_RXD__LPUART2_RX             0x31e
+       //              MX93_PAD_UART2_TXD__LPUART2_TX             0x31e
+       //      >;
+       // };
```