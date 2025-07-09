### 一、安装crowsnest
###### 1、网络安装
A. git clone https://github.com/mainsail-crew/crowsnest.git
B. cd crosnest
C. 修改文件：resources/crowsnest.conf
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
   安装完毕后重启系统

###### 2、本地安装
A. 拷贝 crowsnest-v4.1.14-1-gda74635.tar.bz2 到Model A

B. sudo make install  
   安装完毕后重启系统
  
### 二、查看crowsnest服务
sudo systemctl status crowsnest.service 
服务正常启动则配置完成。如服务启动失败可查看log信息：cat ~/printer_data/logs/crowsnest.log

*注：可通过tools/dev-helper.sh -c 查看摄像头是否支持MJPG编码*

### 三、通过pc机查看摄像头
例如DEBIX Model A的ip为 192.168.2.106，则打开windows浏览器输入：http://192.168.2.106:8554/webcam/?action=stream