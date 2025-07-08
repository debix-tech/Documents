# 🎧 IMX8MP 音频子系统使用说明（HDMI + ES8316）

本平台支持两种音频输出接口：

- **HDMI 音频输出**
- **ES8316 音频编解码器**（通过 I2S 接口，支持耳机/麦克风）





驱动位置：

`sound\soc\fsl\imx-hdmi.c`

`sound\soc\fsl\fsl-asoc-card.c`

`sound\soc\codecs\es8316.c`





查看声卡：

```shell
root@imx8mp-debix:~# cat /proc/asound/cards 
 0 [audiohdmi      ]: audio-hdmi - audio-hdmi
                      audio-hdmi
 1 [es8316audio    ]: es8316-audio - es8316-audio
                      es8316-audio

root@imx8mp-debix:~# aplay -l
**** List of PLAYBACK Hardware Devices ****
card 0: audiohdmi [audio-hdmi], device 0: i.MX HDMI i2s-hifi-0 [i.MX HDMI i2s-hifi-0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: es8316audio [es8316-audio], device 0: HiFi es8316-hifi-0 [HiFi es8316-hifi-0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
root@imx8mp-debix:~# arecord -l
**** List of CAPTURE Hardware Devices ****
card 1: es8316audio [es8316-audio], device 0: HiFi es8316-hifi-0 [HiFi es8316-hifi-0]
  Subdevices: 1/1

```



🔊 音频播放测试

```shell
aplay -D hw:1,0 test.wav
```

表示声卡1，第0个设备也就是es8316audio播放



🎤 录音测试（若连接麦克风）

```shell
root@imx8mp-debix:~# arecord -D plughw:1,0 -f cd -d 5 test.wav
Recording WAVE 'test.wav' : Signed 16 bit Little Endian, Ra[ 1112.315820] GLS_AUDIO spk set on
te 44100 Hz, Stereo

```

