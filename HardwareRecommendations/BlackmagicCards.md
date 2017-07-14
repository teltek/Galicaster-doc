
Blackmagic cards
================

*This page is updated to the 2.0.1 release*

Blackmagic cards are an option to capture high definition contents, both camera and laptop sources. Depending on the card installed and the input type you should be able to configure it following these instructions.

### Driver installation

Blackmagic has partial support for Linux. To install their driver you should download the latest one on:
[http://www.blackmagicdesign.com/support/]

Choose Linux, your card series and your Model and press Search. Download the latest **Desktop Video for Linux**.
To install it, run as root the following commands:

```bash
apt-get install libjpeg62 dkms
dpkg -i <name_of_driver_package.deb>
modprobe blackmagic
```
There is a full guide on how to install the driver and other information on:
[http://documents.blackmagicdesign.com/DesktopVideo/20161007-e10557/Desktop_Video_Manual.pdf]

### Check if the driver and the card are loaded and ready
Run on a terminal:
```bash
lspci | grep Blackmagic
lsmod | grep blackmagic
ls /dev/blackmagic/*
```
You will receive messages like:
```bash
02:00.0 Multimedia video controller: Blackmagic Design Device a11b
blackmagic 2082944 1
/dev/blackmagic/card0
```
### Input configuration
Possible inputs can be listed using:
```bash
gst-inspect1.0 decklinksrc
```
Depending on the card in use and the input select you should be able to select:

#### Connection
Depending on your card connectivity you should be able to choose between:
* sdi
* hdmi
* optical-sdi
* component
* composite
* svideo
Example input = sdi

#### Mode
Choose a value depending on format and framerate, these are listed in full by gst-inspect1.0 :
* pal, ntsc
* 720p50, 720p60
* 1080i50, 1080i60
* 1080p25, 1080p30
Example input-mode = 1080i60

#### Audio
Choose an audio format or leave in auto. On the galicaster plugin for blackmagic we included the option 'none' to avoid recording audio or there is no audio on the HDMI.
* none
* auto
* embedded
* aes
* analog
Example audio-input = auto
