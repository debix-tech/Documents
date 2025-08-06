# ⚙️ Integrating DEBIX Kernel and U-Boot in Yocto Project  

Below explains how to modify kernel and U-Boot source code in a Yocto project to use DEBIX-provided versions.  

## ⚙️ I. Download NXP Yocto Project & DEBIX Kernel/U-Boot Source  

📦 Step 1: Install `repo` Tool  
```shell
mkdir ~/bin
cd ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo > repo
chmod a+x repo
```  
📌 `repo` is Google's multi-repository management tool for fetching Yocto submodules.  

🛠 Step 2: Add Permanent PATH Variable  
Edit `~/.bashrc` and add:  
```shell
export PATH=~/bin:$PATH
```  
Apply changes:  
```shell
source ~/.bashrc
```  

🧾 Step 3: Configure Git Identity  
```shell
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list
```  

🌐 Step 4: Download NXP Yocto Project  
```shell
mkdir imx-yocto-bsp
cd imx-yocto-bsp
repo init -u https://github.com/nxp-imx/imx-manifest.git \
          -b imx-linux-kirkstone \
          -m imx-5.15.71-2.2.0.xml
```
- 📌 This command is based on the **Linux 5.15.71** kernel version.

- `-b` specifies the branch, and `-m` specifies the manifest file.  

To fetch all source code:
```
repo sync
```  

🧰 Step 5: Integrate DEBIX-Specific Kernel & U-Boot  
📁Create local code directory: 
 Create a folder under the imx-yocto-bsp directory to store the DEBIX kernel and U-Boot source code:
```shell
mkdir polyhex-code
cd polyhex-code
```  

⬇️ Download sources:  
- 🐧 **Kernel Source**  
  ```shell
  git clone https://github.com/debix-tech/linux-nxp-debix.git 
  ```
  Switch to the corresponding branch, for example:
  ```
  git checkout lf_5.15.71-debix_model_ab
  ```  
- 🧱 **U-Boot Source**  
  ```shell
  git clone https://github.com/debix-tech/uboot-nxp-debix.git
  ```
  Switch to the corresponding branch:
  ```
  git checkout lf_v2022.04-debix_model_a
  ```  

## 🧩 II. Configure Yocto to Use DEBIX Sources  

🧱 Step 1: Modify U-Boot Recipe (`.bb` file)  
Path: `sources/meta-imx/meta-bsp/recipes-bsp/u-boot/u-boot-imx_2022.04.bb`  

✅ Modify the following fields:
```shell
SRC_URI = "${UBOOT_SRC};branch=${SRCBRANCH}"
UBOOT_SRC ?= "git://${BSPDIR}/polyhex-code/uboot-nxp-debix;protocol=file"
SRCBRANCH = "lf_v2022.04-debix_model_a"
SRCREV = "cf7f1d8c1d3b5b5c2db2b809e1ff1ed79e73ea66"
LOCALVERSION = ""
```  
📌 Key modifications:  
- `UBOOT_SRC` specifies the source path, which points to the local directory containing the U-Boot source.  
*(Make sure to update this according to your actual path.)*

- `SRCBRANCH` specifies the Git branch, e.g., `lf_v2022.04-debix_model_a`.  
*(Update this according to your actual branch.)*

- `SRCREV` specifies the Git commit version.  
*(Be sure to use the correct DEBIX commit ID to avoid build errors.)*

🐧 Step 2: Modify Linux Kernel Recipe  
Path: `sources/meta-imx/meta-bsp/recipes-kernel/linux/linux-imx_5.15.bb`  

✅ Modify the following fields:
```shell
SRCBRANCH = "lf-5.15.y"
LOCALVERSION = ""
KERNEL_SRC ?= "git://${BSPDIR}/polyhex-code/linux-nxp-debix;protocol=file;branch=${SRCBRANCH}"
KBRANCH = "lf_5.15.71-debix_model_ab"
SRC_URI = "${KERNEL_SRC}"
SRCREV = "d740759168c787aaafefd999788db7263fdb471e"
```  
📌 Key modifications:  
* `KERNEL_SRC` defines the source path, pointing to the local Linux kernel directory.  
(*Update according to your actual directory path.*)

* `SRCBRANCH` defines the Git branch, e.g., `lf_5.15.71-debix_model_ab`.  
(*Make sure to update accordingly.*)

* `SRCREV` sets the commit version to download.   
(*Replace with the correct DEBIX commit ID to avoid build errors.*)

## 🔧 III. Recompile  
After making the changes, rebuild the project to apply the new kernel and U-Boot sources.