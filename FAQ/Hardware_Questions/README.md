## DEBIX FAQ - Hardware Questions

**1. ls it possible to connect two or more DEBlX together to make a faster computer?**  
Yes,but you can't  make a powerful compluter by simply bolting it togeher to play games at a faster speed. You can network omputers to build a a cluster computer system, but you need to modify the software to work in this distributed manner.

**2. Where is the power switch?** 
The On/Off and reset buttons are located next to the power supply interface. DEBIX supports Automatic Power On. When you need to shut down the device, if you are using DEBIX Desktop, just click the power button in the upper right corner of the desktop, and then select Shutdown. If you are not using the desktop, you can enter sudo poweroff at the console to shutdown. After the LEDs are off, you should wait one second to ensure that the SD card can complete its wear leveling tasks and write operations. And then you can safely unplug DEBIX. Failure to close DEBIX properly may damage your SD card, which means you must re-mirror it.

**3. Does it support adding additional memory?**  
No, it doesn't. The RAM on DEBIX is a separate chip on the motherboard and cannot be upgraded after purchase.


**4. Why is the clock speed of my DEBIX running slower than advertised?**  
The clock speed is lower than the advertised speed in idle time. As the workload of the CPU increases, the clock speed will increase until it reaches the maximum value (the specific situation varies by CPU model). If the CPU starts to overheat, the situation is more complex: When the device reaches a certain temperature, the clock speed is throttled to prevent overheating.

**5. Does it support overclocking?**  
Yes, it supports. But overclocking will void your warranty. Due to the way silicon chips are produced, each device supports a different degree of overclocking. For a capable and stable system, we recommend that you do not overclock your DEBIX.

**6. Does the HDMI port support CEC?**  
Yes, it does.
 
**7. Does DEBIX support VGA?**  
DEBIX displays support various video signals including but not limited to VGA and HDMI inputs, but DEBIX computers do not have built-in VGA ports. To use VGA:
- Use an active HDMI-to-VGA adapter (passive cables will not work).
- Ensure the adapter has external power (unpowered adapters will not function properly).

**8. Does it support adding a touch panel?**  
Yes, it does.

**9. Does it support sound transmission via HDMI?**  
Yes.

**10. How about standard audio input and output?**  
There is a standard 3.5mm interface for audio output (speaker). You can add any supported USB microphone, or you can use the I2S interface to add a codec for additional audio I/O.


**11. Can I power the motherboard through a USB hub?**  
It depends on the USB hub. Some hubs comply with the USB 2.0 standard and only provide 500mA per port, which is not enough to power your DEBIX.

**12. Can I use the battery or wall socket to power DEBIX?**  
Running DEBIX directly on the battery requires more attention, and it may damage your DEBIX. However, if you are a practised user, you can give it a try. For example, the four most common AA rechargeable batteries can provide 4.8V when fully charged. Technically 4.8V is just within the tolerance of DEBIX, but as the battery runs out, the system quickly becomes unstable. While four AA alkaline (non-rechargeable) batteries can provide 6V voltage, which exceeds the acceptable tolerance range and may damage your DEBIX. By using a buck and/or boost circuit, you can ensure stable 5V voltage (or using a charger set specifically designed to output a stable 5V from several batteries). These devices are usually sold as emergency battery chargers for mobile phones.
 
**13. Is Power Over Ethernet (POE) feasible?**  
Yes, but it need to be equipped with a POE power supply module.

**14. What size SD card is needed?**  
Micro SD card.

**15. What capacity of SD card does it support?**  
Although the minimum capacity of 8GB should be enough for most people, we have tried SD cards up to 128GB and they all work well. You can also connect a USB flash disk or mobile hard disk to provide additional storage capacity.

**16. Can I boot DEBIX through a USB-connected hard disk instead of an SD card?**  
No, it doesn’t support.

**17. Does it has built-in wireless network?**  
DEBIX has built-in 2.4G & 5G WiFi.

**18. Does it has built-in bluetooth?**  
There’s a built-in bluetooth 5.0.

**19. What models of cameras are supported?**  
OV5640, etc.

**20. How about the resolution?**  
DEBIX supports maximum resolution of 4kp60 and it has superb codecs (h.265, h.264, VP9...).

**21. Does DEBIX only support one display when I play video in full screen?**  
The DEBIX Model A/B/Infinity supports triple-screen or dual-screen display via HDMI/LVDS/MIPI interfaces, defaulting to extended mode.

**22. What is the touch rotation angle of the touch screen?**  
90 degrees.

**23. Does it support networking？**  
Yes, it supports. DEBIX has 1000BaseT wired Ethernet and one network interface (pin headers) without network compiler.

**24. How do I connect a mouse and keyboard?**  
Please refer to DEBIX manual document on [official website](https://www.debix.io/).

**25. Is there a GPU binary?**  
Yes

**26. Can I add a touchscreen?**  
Yes
 
**27. Is sound over HDMI supported?**  
Yes

**28. What about standard audio in and out？**  
3.5mm audio interface

**29. How to use DEBIX Model A for 5V CAN communication?**  
It needs to be used in conjunction with a CAN transceiver peripheral for CAN communication, such as DEBIX I/O Board, or other CAN transceiver modules.

<div align="right">  

[▲ Return to the Top](#debix-faq---hardware-questions)
</div>