### Converting DEBIX Model C's UART Debug Port to General-Purpose UART  

This tutorial shows how to disable the default serial debug console and repurpose UART (e.g., LPUART1) as a standard serial device for user applications.  

🧱 **1️⃣ Modify U-Boot: Disable Serial Console Output**  
📁 Edit the file:  
```
include/configs/imx93_evk.h
```  
🔧 Change the original console parameter:  
```c  
"console=ttyLP0,115200 earlycon\0"  
```  
✅ Modify to:  
```c  
"console=tty0,115200 earlycon\0"  
```  
📌 **Explanation**:  
- `ttyLP0` is the default serial console  
- Changing to `tty0` redirects console output to **graphical terminal or null terminal**, freeing `ttyLP0` for user applications  

🧬 **2️⃣ Modify Linux Kernel: Release UART Occupancy in DTS**  
📁 Edit DTS file:  
```
arch/arm64/boot/dts/freescale/imx93-11x11-evk.dts
```

✅ Comment out:  
```dts  
stdout-path = &lpuart1;  
```