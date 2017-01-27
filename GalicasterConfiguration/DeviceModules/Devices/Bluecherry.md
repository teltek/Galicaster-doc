Bluecherry PV and BC cards
==========================

### Drivers & information
Bluecherry cards are supported by Linux, both SD capturing PV cards and HW encoding BC PCIe. PV cards are SD capturing cards with multiple inputs (tipically 4) via BNC connectors. Some models also supports audio capturing.

BC cards are Hardware Compression (mpeg4 or h264) cards oriented to surveillance purposes. Since they have V4l2 interface support they represent a alternative solution for Hardware encoding, however, encoded resolution is limited to 320x204.

* [Driver installation](#driver-installation)
* [Device identification](#device-identification)
* [Device configuration](#device-configuration)
* [Module configuration](#module-configuration)
* [Troubleshooting](#troubleshooting)
* [FAQ](#faq)

### Technical data
* Vendor: [Bluecherry](http://store.bluecherry.net/)
* Models [*PV](http://store.bluecherry.net/capture-cards/video4linux-supported) and [BC](http://www.bluecherrydvr.com/products/hardware-compression-h-264-capture-card-pcie-x1/) models
* Format: **YUV**
* Connector: **BNC**
* Signal: **RAW**
* Drivers: PV pre-installed
* BC models available [here](https://github.com/bluecherrydvr/solo6x10)
* Plugin: [v4l2](../V4L2.md)
* Price: **from 50 to 500 €**


### Driver installation
For PV models, drivers already present on the linux kernel - bttv.  
For BC models - hardware compression - do the following.

* Download the lattest version at [Bluecherry's download area](http://downloads.bluecherrydvr.com/solo6x10/) or at [Bluecherry's Github](https://github.com/bluecherrydvr/solo6x10).
* Compile the driver: run make
* Install it, running as root: `sudo make install && sudo depmod -a`
* Restart the computer.


### Device identification
1. Find the Device name attribute:
  * `udevadm info --attribute-walk --name=/dev/video0 | grep name`
    * Usual Device IDs:
    * PV-143 : BT878 video (ProVideo PV143)
    * BC multiple cameras : solo6x10-edge
    * BC single cmaera : solo6x10-edge-enc
1. Fix access path
  * Create or modify the file ``/etc/udev/rules.d/galicaster.rules`.
  * Add the line: `KERNEL=="video[0-9]*", ATTR{name}=="BT878 video (ProVideo PV143)", GROUP="video", SYMLINK+="bluecherry"`
    * Change the name Attribute depending on your card

### Device configuration
#### BC cards
Check wheter the card and the driver are installed properly.
```bash
lspci | grep Bluecherry
lsmod | grep solo6x10
```
PENDING

#### PV-Cards
For input 1 and Standard PAL-BG
```bash
v4l2-ctl -d /dev/bluecherry -i 0 -s 5
```

### Module configuration
#### Admitted values:
* `name`: Name assigned to the device.
* `device`: Device type: **v4l2**
* `flavor`: Matterhorn "flavor" associated to the track. (**presenter**|presentation|other)
* `location`: Device's mount point in the system (e.g. `/dev/video0 or /dev/webcam`).
* `file`: The file name where the track will be recorded. (default:`CAMERA.avi`)
* `videocrop`: Margin in pixels to be cutted. Useful to set a 4:3 proportion on a HD webcam.videocrop-top, videocrop-bottom, videocrop-left, videocrop-right. (optional)
* `caps`: GStreamer cappabilities of the device (mimetype=TYPE, framerate=X/Y,width=A,height=B)


#### Example:
```ini
[track1]
name = Camera
device = v4l2
flavor = presenter
location = /dev/camera
file = CAMERA.avi
caps = video/x-raw-yuv,framerate=30/1,width=720,height=576
videocrop-left = 0
videocrop-right = 0
```

### Troubleshooting

### FAQ
