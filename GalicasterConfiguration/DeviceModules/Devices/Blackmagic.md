Blackmagic capture cards
========================

*This page is updated to the 2.0.1 release*

### Drivers & information
Blackmagic Design provides linux support for their Intensity, Decklink and Multibridge series.
Blackmagic capture cards support multiple formats - through adaptors - including HD-SDI and HDMI. Check the table below for more information on connectors and signal standards available.

* [Models table](#models-table)
* [Driver installation](#driver-installation)
* [Device identification](#device-identification)
* [Module configuration](#module-configuration)
* [Troubleshooting](#troubleshooting)
* [FAQ](#faq)

#### Technical data
* Vendor: [Blackmagic Design](http://www.blackmagicdesign.com/)
* Models **Intensity Pro, Decklink SDI and, Multibride**
* Resolution: **upto Full HD**
* Format: **SDI, HDMI and others**
* Connector: **BNC or HDMI**
* Signal: **RAW**
* Drivers: available [here](http://www.blackmagicdesign.com/support/)
* GC Module: [blackmagic](../Blackmagic.md)
* Price: **around 300 €**

### Models table

| Model | Singal standards | Connectors | Audio | HD formats | SD formats | HW Encoding | Price |
|-----|-----|-----|-------|-------|---------|------|-------------|
| [Intensity Pro](http://www.blackmagicdesign.com/products/intensity/) | HDMI <br> Components <br> Composite <br> S-Video | HDMI <br> Components | embedded <br> stereo RCA | 1080p (@23.98, 24, 25, 29.97, 30) <br> 1080i (@50, 59.94, 60) <br> 720p (@50, 59.94, 60)	PAL 625 | PAL 625 <br> NTSC 525 | No | 200 $ |
| [Decklink SDI](http://www.blackmagicdesign.com/products/intensity/) | SDI <br> Components <br> Composite <br> S-Video | BNC | embedded <br> stereo RCA | 1080p (@25, 29.97,30) <br> 1080i (@50, 59.94, 60) <br> 1080PsF (23.98, 24 ,25, 29.97, 30 ) <br> 720p (@50, 59.94, 60)	PAL 625 | PAL 625 <br> NTSC 525| No | 300 $ |

Table information retrieved from:

* http://www.blackmagicdesign.com/products/intensity/techspecs
* http://www.blackmagicdesign.com/products/decklink/techspecs

### Driver installation
To install their driver you should download the latest one on:
 http://www.blackmagicdesign.com/support/

On the form Choose Linux, your card series and your Model and press Search. Download the latest **Desktop Video for Linux**.
To install it, double-click on the DEB package or run as root the following commands:

```bash
apt-get install libjpeg62 dkms
dpkg -i <name_of_driver_package.deb>
modprobe blackmagic
```

There is a full guide on how to install the driver and other information on:
http://documents.blackmagicdesign.com/DesktopVideo/20161007-e10557/Desktop_Video_Manual.pdf

#### Check if the driver and the card are loaded and ready
Run on a terminal:
```bash
lspci | grep Blackmagic
lsmod | grep blackmagic
ls /dev/blackmagic*
```
You will receive messages like:
```bash
_02:00.0 Multimedia video controller: Blackmagic Design Device a11b_
_blackmagic                   2082944  1_
/dev/blackmagic0
```

### Device identification
This device doesn't need to be identified, it's accessed directly by Gstreamer. However, if multiple Blackmagic cards are installed the device number has to be indicated on the configuration as subdevice. Otherwise the _subdevice default value will work just fine.

```bash
ls /dev/blackmagic/*
/dev/blackmagic/card0
*subdevice = 0*
```

### Module configuration
#### Admitted values:

* `name`: Name assigned to the device.
* `device`: Device type: **rtp**
* `flavor`: Matterhorn "flavor" associated to the track. (**presenter**|presentation|other)
* `location`: Device's mount point in the system (e.g. /dev/blackmagic0).
  * In this module plugin this parameter is merely informative.
* `file`: The file name where the track will be recorded. (default:CAMERA.avi)
* `input`: The type of connection used. (sdi/hdmi/optical-sdi/component/composite/svideo)
* `input`-mode: Format and framerate of the input:
  * (ntsc|ntsc2398|pal|ntsc-p|pal-p|720p50|720p5994|720p60|**1080p25**|1080p2398|1080p24|1080p2997|1080p30|1080p50|1080p5994|1080p60|1080i50|1080i5994|1080i60)
  * "i" stands for interlaced, "p" stand for progressive
* `subdevice`: Determines which blackmagic card to use if more than one is installed. (**0**/1/2/3)
* `audio`: audio format. (none/**|auto**/|embedded/|aes/|analog)
  * `vumeter`: Whether the audio input would be represented on the vumeter. (**True**|False)
  * `player`: Whether the audio input would be played on preview. (**True**|False)
  * `amplification`: Gstreamer amplification value: < 1 decreases and > 1 increases volume. Values between 1.0 and 2.0 are commonly used. (default:**1.0**)

For more information on mode, connection and audio values please use:
```bash
gst-inspect1.0 decklinksrc
```

Example:
```ini
[track1]
name = Blackmagic
device = blackmagic
flavor = presenter
location = /dev/blackmagic0
file = CAMERA.avi
input = sdi
input-mode = 1080p50
subdevice = 0
audio-input = auto
vumeter = True
player = True
amplification = 1.0
```

### Troubleshooting
**No black screen if no input on startup**  
A know issue of blackmagic cards is that if the card doesn't have input when the system is booted no input comes in. The expected behavior should be to get a black screen instead. If any input is received and later on unplugged, then the card do provides the black screen.

**Incompatibility with Epiphan framegrabbers**  
Due to a conflict between the drivers of Blackmagic and Epiphan cards drivers, their devices are incompatible one to the other. Combinations of these devices with ones or other vendor others has been succesfully tested.

### FAQ
1. Is possible to use more than one Blackmagic card on the same computer?
  * Yes, up to 4 different cards, you have to use the subdevice parameter in order to select different cards. However, depending on your hadware, you may be limited to 2 or 3 for recording purposes.
1. I've configured the card and I get video but it is jumpy and broken. What's the matter?
  * The card is capable to provide video in some cases when the format is wrong but similar to the right one. For example, 108p50 and 1080p60 will get video when crossmatched.
