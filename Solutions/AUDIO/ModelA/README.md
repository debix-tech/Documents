# 🎧 IMX8MP Audio Subsystem User Guide (HDMI + ES8316)

This platform supports two types of audio output interfaces:

* **HDMI Audio Output**
* **ES8316 Audio Codec** (via I2S interface, supports headphones/microphone)

---

### Driver Locations:

* `sound/soc/fsl/imx-hdmi.c`
* `sound/soc/fsl/fsl-asoc-card.c`
* `sound/soc/codecs/es8316.c`

---

### Check Available Sound Cards:

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

---

### 🔊 Audio Playback Test

```shell
aplay -D hw:1,0 test.wav
```

This command uses sound card 1, device 0 — i.e., **es8316audio** — for audio playback.

---

### 🎤 Audio Recording Test (if a microphone is connected)

```shell
root@imx8mp-debix:~# arecord -D plughw:1,0 -f cd -d 5 test.wav
Recording WAVE 'test.wav' : Signed 16 bit Little Endian, Ra[ 1112.315820] GLS_AUDIO spk set on
te 44100 Hz, Stereo
```

---
