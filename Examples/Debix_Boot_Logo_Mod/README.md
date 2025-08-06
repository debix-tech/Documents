### Changing the Boot Logo for DEBIX Boards (Applicable to DEBIX Model A)  

✅ **Step 1: Download DEBIX’s official kernel source code**  
Code repository: https://github.com/debix-tech  
📥 Download command:  
```shell  
git clone --depth=1 https://github.com/debix-tech/linux-nxp-debix.git  
```  

✅ **Step 2: Prepare a new logo image (`.ppm` format)**  
Command to convert PNG to PPM on Ubuntu 22.04:  
```shell  
pngtopnm <input.png> > <output.pnm>  
```  
Convert the image to 224 colors:  
```shell  
ppmquant 224 <input.pnm> > <output.pnm>  
```  
Convert the 224-color image to ASCII plain format:  
```shell  
pnmtoplainpnm <input.pnm> > <output.ppm>  
```  
Finally, verify the format using `file <name.ppm>`. The output should be:  
`Netpbm image data, size = [width] x [height], pixmap, ASCII text`.  

✅ **Step 3: Replace the default logo file in the kernel**  
Overwrite the default logo in the kernel source directory with your prepared file:  
```shell  
drivers/video/logo/logo_linux_clut224.ppm  
```  
Rename your prepared `logo.ppm` to `logo_linux_clut224.ppm` before replacement.  

⚠️ **Notes**:  
- Filename **must** be: `logo_linux_clut224.ppm`  
- Format **must** be ASCII PPM with ≤ 224 colors.  

✅ **Step 4: Recompile the kernel and replace the image**  
Recompile the kernel:  
```shell  
make -j4  
```  
After compilation, locate the `Image` file under `arch/arm64/boot`, replace it on the TF card, and reboot the DEBIX.