Osprey Cards
============

**NOT TESTED WITH GALICASTER 2**

### Drivers & information
Osprey cards are analog video captures on both PAL and NTSC (including panoramic). They work with composite a S-Video inputs and balanced audio input.

* [Driver installation](#driver-installation)
* [Device identification](#device-identification)
* [Device configuration](#device-configuration)
* [Module configuration](#module-configuration)
* [Troubleshooting](#troubleshooting)
* [FAQ](#faq)

### Technical data
* Vendor: [Viewcast](http://www.viewcast.com/)
* Models: [230](http://www.viewcast.com/products/osprey-cards/osprey-230), [100](http://www.viewcast.com/products/osprey-cards/osprey-100), [100e](http://www.viewcast.com/products/osprey-cards/osprey-100e), [210](http://www.viewcast.com/products/osprey-cards/osprey-210), [260e](http://www.viewcast.com/products/osprey-cards/osprey-260e), [440](http://www.viewcast.com/products/osprey-cards/osprey-440), [460e](http://www.viewcast.com/products/osprey-cards/osprey-460e) and [530](http://www.viewcast.com/products/osprey-cards/osprey-530)
* Resolution: **PAL/NTSC**
* Format: **Svideo or Composite**
* Connector: **BNC** and other through adaptors
* Signal: **RAW**
* Drivers: **PCI-based pre-installed
on Ubuntu 12**
* Plugin: [v4l2](../V4l2.md)
* Price: **From $170 (Osprey 100)
to $1000 (Osprey 530)**


### Driver installation
For PCI cards, the driver is included in the linux kernel - bttv.
For PCIe cards, the driver can be found at [kernellabs.com](http://www.kernellabs.com/blog/)

### Device identification
1. Find the Device name attribute:
  * `udevadm info --attribute-walk --name=/dev/video0 | grep name`
    * Usual Device IDs:
      * BT878 video (Osprey 210/220/230
1. Fix access path
  * With sudo create or modify the file `/etc/udev/rules.d/galicaster.rules`
  * Add the line: `KERNEL=="video[0-9]*", ATTR{name}=="BT878 video (Osprey 210/220/230", GROUP="video", SYMLINK+="osprey"`

### Device configuration
Osprey cards can capture svideo and composite with NTSC, PAL and SECAM formats. To probe and set the parameters use the video4linux2 CLI configuration and compound your configuration on a script:
To list the parameters:

* Inputs
  * `v4l2-ctl -d /dev/osprey -n`
* Standards
  * `v4l2-ctl -d /dev/osprey --list-standards`

Useful commands
* PAL over SVIDEO: _v4l2-ctl -d /dev/osprey -i 1 -s 4

### Module configuration
#### Admitted values:
* `name`: Name assigned to the device.
* `device`: Device type: v4l2
* `flavor`: Matterhorn "flavor" associated to the track. (`presenter`|`presentation`|`other`)
* `location`: Device's mount point in the system (e.g. `/dev/video0 or /dev/webcam`).
* `file`: The file name where the track will be recorded.
* `videocrop`: Margin in pixels to be cutted. videocrop-top, videocrop-bottom, videocrop-left, videocrop-right (optional).
* `caps`: GStreamer cappabilities of the device (mimetype=TYPE, framerate=X/Y,width=A,height=B)

#### Caps magic
* type: video/x-raw
* framerate: 25/1
* resolution:
regular (4:3) : NTSC width=720, height=480 PAL width=720,height=576
panoramic (16:10): NTSC width=924,height=480 PAL width=924,height=576
For more information http://pygstdocs.berlios.de/pygst-tutorial/capabilities.html

#### Example:
```ini
[track1]
name = Osprey
device = v4l2
flavor = presenter
location = /dev/osprey
file = CAMERA.avi
caps = video/x-raw,framerate=25/1,width=720,height=576
```

### Troubleshooting

### FAQ
