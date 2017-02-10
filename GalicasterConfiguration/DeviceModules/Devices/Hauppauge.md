
Hauppauge capture card
======================

**_NOT TESTED WITH GALICASTER 2.X_**  
*This page is updated to the 1.4.2 release*

### Drivers & information
Hauppage cards models PVR-350 and PVR-250 (among others) are hardware capture cards. Cameras and other devices can connect to a Hauppauge card through a SVideo or RCA connector (last only PVR-350) and a Line Level audio input.
They are compatible with both PAL and NTSC. They provide RAW input (for both audio and vide), and MPEG2 encoded input.

* [Driver installation](#driver-installation)
* [Device identification](#device-identification)
* [Device configuration](#device-configuration)
* [Module configuration](#module-configuration)
* [Troubleshooting](#troubleshooting)
* [FAQ](#faq)

### Technical data
* Vendor: **Hauppage**
* Models **PV·-350, PVR-250, HVR-1600**
* Resolution: **PAL/NTSC**
* Format: **PAL/NTSC** [raw or mpeg2*
* Connector: **RCA or SVideo and mini-jack** (3,5mm)
* Signal: Composite or Svideo
* Drivers: **pre-installed on Ubuntu 12**
* Plugin: [hauppauge](../Hauppauge.md) or [v4l2](../V4L2.md)
* Price: Obsolete, consult stock.



### Driver installation
The driver is included in the linux kernel - ivtv.

### Device identification
1. Find the Device name attribute:
  * `udevadm info --attribute-walk --name=/dev/video0 | grep name`
    * Usual Device IDs:
      * Encoded input: `ivtv0 encoder MPG`
      * Raw input: `ivtv0 encoder YUV`
      * Audio raw input: `ivtv0 encoder PCM`
1. Fix access path
  * With sudo create or modify the file `/etc/udev/rules.d/galicaster.rules`
  * Add the following lines:
  ```bash
KERNEL=="video[0-9]*", ATTR{name}=="ivtv0 encoder MPG", GROUP="video", SYMLINK+="haucamera"
KERNEL=="video[0-9]*", ATTR{name}=="ivtv0 encoder YUV", GROUP="video", SYMLINK+="hauprevideo"
KERNEL=="video[0-9]*", ATTR{name}=="ivtv0 encoder PCM", GROUP="audio", SYMLINK+="haupreaudio"
```

### Device configuration
To set the parameters use the video4linux2 CLI configuration and compound your configuration on a script:

To list the parameters:

* `v4l2-ctl -d /dev/video0 -L`

Useful commands

* Select composite input:
  * `v4l2-ctl -d /dev/haucamera -i 1`  
  * `v4l2-ctl -d /dev/haucamera -i 3`
* Select svideo input
  * `v4l2-ctl -d /dev/haucamera -i 2`
  * `v4l2-ctl -d /dev/haucamera -i 4`
* Select NTSC/PAL or SECAM
  * Consult standard: `v4l2-ctl -d /dev/haucamera --list-standards`
  * Assign statndard: `v4l2-ctl -s 1`

### Module configuration
#### Admitted values:
* `name`: Name assigned to the device.
* `device`: Device type: hauppauge
* `flavor`: Matterhorn "flavor" associated to the track. (`presenter`|`presentation`|`other`)
* `location`: Device's mount point of the MPEG output
* `locprevideo`: Device's mount point of the RAW output for preview.
* `locpreaudio`: Device's mount point of the PCM output for preview.
* `file`: The file name where the track will be recorded.
* `vumeter`: Whether the audio input would be represented on the vumeter. (`True`|`False`)
* `player`: Whether the audio input would be played on preview. (`True`|`False`)

##### Example:
```ini
[track1]
name = Hauppauge
device = hauppauge
flavor = presenter
location = /dev/haucamera
locpreavideo = /dev/hauprevideo
locpreaudio = /dev/haupreaudio
file = CAMERA.mpg
vumeter = True
player = True
```

### Troubleshooting
**The driver doesn't change the input when active.**  
Unlike other v4l2 compatible devices, Hauppauge won't accept changes on the driver configuration when is being accesed. To change configuration paramaters, the resources have to be liberated and then confuration can be modified.
Try loading the default profile, change the input manually (v4l2-ctl) and load the profile again.

**Audio input only for one channel**  
Default configuration on hauppauge may present audio mono, then only one channel will be recorded. Check the V4L2 parameters of the driver and set the configuration to stereo.

```bash
v4l2-ctl -d /dev/haucamera -L
audio_stereo_mode (menu)   : min=0 max=3 default=0 value=0 flags=update
				0: Stereo
				1: Joint Stereo
				2: Dual
				3: Mono
v4l2-ctl -d /dev/haucamera --set-ctrl=audio_stereo_mode=0
```
**Error loading driver**  
If you experience loading the driver - reported in dmesg or syslog, first of all, check if the card is properly connected. If the problem still remains, try changing the card to another PCI slot. In the last case, force the driver identification of the card manually, create the file `_/etc/modprobe/hauppauge.conf` and include the line:

`options ivtv cardtype=2`  
"2" for Hauppauge PVR-350 and "1" for PVR-250

### FAQ
**I only want to record video**  
If you only want to record video with a Hauppauge card you better use it with the v4l2 plugin with the following paramters:

```ini
location=dev/haucamera
caps=_video/x-raw,framerate=25/1,width=720,height=576 #if PAL
caps=_video/x-raw,framerate=30000/1001,width=720,height=480 #if NTSC
```
Note_: 30000/1001 is 29.97 fps_

**I want a different encoding than MPEG2**  
To encode the video in a different format you have to discard the hardware encoding and use Hauppauge with v4l2 plugin. In that case, audio has to be recorded through the sound card. Use the parameters in the previous question.
