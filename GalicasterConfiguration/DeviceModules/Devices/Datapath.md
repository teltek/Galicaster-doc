
Datapath video capture cards
============================

### Drivers & information
Datapath cards are VGA and DVI capturing devices. They capture up to 1080p DVI and 2048x1536 analog. They also provide a blank signal when signal is missing and scales the resolution if a change occur.

* [Drivers & information]()
* [Driver installation]()
* [Device identification]()
* [Device configuration]()
* [Module configuration]()
* [Troubleshooting]()
* [FAQ]()

### Technical data
* Vendor: [Datapath]()
* Models [VisionRGB-E1S]()
* Resolution: **upto Full HD**
* Format: **YUV or JPEG**
* Connector: **DVI**
* Signal: **RAW**
* Drivers: available [here]()
* Plugin: [v4l2]()
* Price: **around 650 €**

### Driver installation
Links and instructions to install the linux driver for Datapath are available at http://www.datapath.co.uk/linux-driver

﻿To install the driver unpack the zipped tarball and execute the script at `scripts/install.kernel` **as root**.
Further information can be found in the installation help file, `docs/INSTALL`.

To uninstall the driver execute `scripts/uninstall.sh`

### Device identification
1. Find the Device name attribute:
  * `udevadm info --attribute-walk --name=/dev/video0 | grep name`
    * rgb133 (0-0)
1. Fix access path
  * Create or modify the file `/etc/udev/rules.d/galicaster.rules.`
  * Add the line: `KERNEL=="video[0-9]*", ATTR{name}=="rgb133 (0-0)", GROUP="video", SYMLINK+="screen"`

### Device configuration

### Module configuration
#### Admitted values:
* `name`: Name assigned to the device.
* `device`: Device type: **v4l2**
* `flavor`: Matterhorn "flavor" associated to the track. (**presenter**|presentation|other)
* `location`: Device's mount point in the system (e.g. /dev/screen).
  * In this plugin this parameter is merely informative.
* `file`: The file name where the track will be recorded. (default:`CAMERA.avi`)
* `videocrop`: Margin in pixels to be cutted. Useful to set a 4:3 proportion on a HD webcam. `videocrop-top`, `videocrop-bottom`, `videocrop-left`, `videocrop-right` (optional).
* `caps`: GStreamer cappabilities of the device (`mimetype=TYPE, framerate=X/Y,width=A,height=B`)

#### Caps magic:
* type: video/x-raw-yuv
* framerate: 30/1, 25/1, 10/1 ...
**. Datapath provides an stable 30 fps, lower framerates will decimate the input signal accordingly.
* resolution:
  * width=800,height=600, width=640,height=480, width=1024,height=768
  * panorarmic: width=1280,height=720 or width=1920,height=1080
* Use guvcview to know wich capabilities are compatible with your device.
For more information http://pygstdocs.berlios.de/pygst-tutorial/capabilities.html

#### Example:
```ini
[track1]
name = Datapath
device = datapath
flavor = presentation
location = /dev/screen
file = SCREEN.avi
caps = video/x-raw-yuv,framerate=30/1,width=1280,height=720
videocrop-left = 0
videocrop-right = 0
```

### Troubleshooting
**16:9 resolutions aspect is deformed**
You should establish a 16:9 resolution on the configuration. Changing sources of different aspect ratios will deform one type or another.

**When I resume a recording after pausing without signal it fails**
Unfortunatelly, the absence of singal after pause make the driver fails. To avoid losing signal use a VGA scaler with signal replacement cappabilities

**If the connector is unplugged several times the recording fails**
Update your driver to the newest one. Old drivers didn't handled unplugging efficiently.

### FAQ
1. **Can I change the NO SIGNAL message?**  
Yes, you can modifying the driver configuration. When the driver is installed a sample with instruction is placed at `etc/modprobe.d/rgb133.sample.conf`
