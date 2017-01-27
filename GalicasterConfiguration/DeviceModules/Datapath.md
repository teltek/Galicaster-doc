
Datapath device module
======================

**THIS PAGE IS UNDER CONSTRUCTION**

The Datapath device module is a modificiation of the [V4L2 module](v4l2.md), the most generic device module on Galicaster. For more detailed information check out each device page or contact the [Community spaces](https://wiki.teltek.es/display/Galicaster/Community).

The Datapath device module includes certain features:

* Cropping
* Mjpeg recording
* Framerate safeguard - to prevent dropped frames.

### Module Compatibility
* [Datapath VisionRGB-E1S](Devices/Datapath.md)

### Module configuration
Admitted values:

* `name`: Name assigned to the device.
* `device`: Device type: datapath
* `flavor`: Matterhorn "flavor" associated to the track. (`presenter`|`presentation`|`other`)
* `location`: Device's mount point in the system (e.g. `/dev/video0`).
* `file`: The file name where the track will be recorded. (The path is automatically assembled)
* `videocrop`: Margin in pixels to be cutted. Useful to set a 4:3 proportion on a HD webcam.videocrop-top, videocrop-bottom, videocrop-left, videocrop-right (optional).
* `caps`:  GStreamer cappabilities of the device. Check the [caps section](#caps) for more information.

Use GVUCView tool to know wich capabilities are compatible with your device
For more information  http://pygstdocs.berlios.de/pygst-tutorial/capabilities.html

### Caps
V4L2 devices accepts two types of signal inputs - RAW and MJPEG - and multiple resolution-framerate combinations. A simplified Gstreamer cappabilities string is formed by type, resolution and framerate among other parameters:

* **Type**: `image/jpeg` | `video/x-raw-yuv`
* **Framerate**: X/Y. Examples: 30/1, 25/1, 24/1, 10/1
* **Resolution**: width=A,height=B. A and B being length in pixels

Them, a complete caps string looks like:
```ini
image/jpeg, framerate=24/1, width=1280, height=720
video/x-raw-yuv framerate=30/1, width=1280, height=1024
```
Examples:
For a Datapath RGBVision e1s
```ini
[track1]
name = Slides
device = v4l2
location = /dev/datapath
file = SCREEN.avi
flavor = presentation
caps = video/x-raw-yuv,framerate=30/1,width=1024,height=768
```
