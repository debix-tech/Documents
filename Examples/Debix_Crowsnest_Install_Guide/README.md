### 1. Installing crowsnest
###### 1. Network Installation
A. git clone https://github.com/mainsail-crew/crowsnest.git  
B. cd crosnest  
C. Modify the file: resources/crowsnest.conf  
```
--- a/resources/crowsnest.conf
+++ b/resources/crowsnest.conf
@@ -31,15 +31,15 @@
 [crowsnest]
 log_path: %LOGPATH%
 log_level: verbose                      # Valid Options are quiet/verbose/debug
-delete_log: false                       # Deletes log on every restart, if set to true
-no_proxy: false                         # If set to true, no reverse proxy is required. Only change this, if you know what you are doing.
+delete_log: true                       # Deletes log on every restart, if set to true
+no_proxy: true                         # If set to true, no reverse proxy is required. Only change this, if you know what you are doing.

 [cam 1]
 mode: ustreamer                         # ustreamer - Provides MJPG and snapshots. (All devices)
                                         # camera-streamer - Provides WebRTC, MJPG and snapshots. (only RPiOS + RPi 0/1/2/3/4)
-port: 8080                              # HTTP/MJPG stream/snapshot port
-device: /dev/video0                     # See log for available devices
-resolution: 640x480                     # <width>x<height> format
+port: 8554                              # HTTP/MJPG stream/snapshot port
+device: /dev/video2                     # See log for available devices
+resolution: 1920x1080                     # <width>x<height> format
 max_fps: 15                             # If hardware supports it, it will be forced, otherwise ignored/coerced.
 #custom_flags:                          # You can run the stream services with custom flags.
 #v4l2ctl:                               # Add v4l2-ctl parameters to setup your camera, see log for your camera capabilities.

```
D. sudo make install  
   Restart the system after the installation is complete.

###### 2. Local Installation
A. Copy crowsnest-v4.1.14-1-gda74635.tar.bz2 to Model A  

B. sudo make install  
   Restart the system after the installation is complete.  


### 2. Checking the crowsnest Service
sudo systemctl status crowsnest.service  
If the service starts normally, the configuration is complete. If the service fails to start, you can check the log information: cat ~/printer_data/logs/crowsnest.log  

*Note: You can check if the camera supports MJPG encoding via tools/dev-helper.sh -c*  


### 3. Viewing the Camera via PC
For example, if the IP address of DEBIX Model A is 192.168.2.106, open a Windows browser and enter: http://192.168.2.106:8554/webcam/?action=stream