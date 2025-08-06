## 🎮 Connect and Test Xbox Controller on DEBIX  

### 🧱 Step 1: Install Xbox Controller Driver  
```shell
sudo apt-get install xboxdrv
```  
📌 `xboxdrv` is a universal driver supporting Xbox 360/Xbox One controllers (wired or wireless).  

### 🚫 Step 2: Disable Bluetooth Enhanced Retransmission Mode (ERTM)  
ERTM may interfere with Xbox Bluetooth connections and must be disabled:  
```shell
echo 'options bluetooth disable_ertm=Y' | sudo tee -a /etc/modprobe.d/bluetooth.conf
```  

### 🔄 Step 3: Reboot DEBIX Device  
```shell
sudo reboot
```  

### 📡 Step 4: Connect Xbox Controller via Bluetooth  
```shell
sudo bluetoothctl
```  
Execute in Bluetooth interactive mode:  
```shell
scan on                             # Start device scanning
connect XX:XX:XX:XX:XX:XX           # Replace with controller's MAC address
quit                                # Exit after successful connection
```  

### 🎛️ Step 5: Install Joystick Testing Tool  
```shell
sudo apt-get install joystick
```  
This tool includes the `jstest` command for detecting controller input signals..  

### 🖥️ Step 6: Install GUI Testing Tool (Optional)  
```shell
sudo apt-get install jstest-gtk
```  
Run with:  
```shell
jstest-gtk
```  
📊 Visually monitor button, joystick, and trigger states.  

### 🎮 Step 7: Test Xbox Controller via Command Line  
```shell
sudo jstest /dev/input/js0
```  
✅ Successful recognition shows real-time output like:  
```shell
Driver version is 2.1.0.
Joystick (Microsoft X-Box 360 pad) has 8 axes and 11 buttons.
```  
