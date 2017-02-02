Axis Network Cameras
====================
**NOT TESTED WITH GALICASTER 2**  
**THIS PAGE IS UNDER CONSTRUCTION**

### Drivers & information
Based on open IP standards, Axis network cameras connect to any kind of IP network, including the Internet, and enable remote viewing and recording from anywhere.

* [Driver installation](#driver-installation)
* [Device identification](#device-identification)
* [Device configuration](#device-configuration)
* [Module configuration](#module-configuration)
* [Troubleshooting](#troubleshooting)
* [FAQ](#faq)

#### Technical data
* Vendor: [Axis](http://www.axis.com/products/video/camera/)
* Models **Fixed, dome, PTZ and Thermal models**
* Resolution: **up to Full HD**
* Format: **MPEG4 or H264**
* Connector: **Ethernet**
* Signal: **RTSP**
* Drivers: **pre-installed on Ubuntu 12**
* Plugin: [Rtpvideo](../RTP.md)
* Price: **from 100 to 3000€**  depending on the model


### Driver installation
The driver is included in the Linux kernel.

### Device identification

### Device configuration

### Module configuration
#### Admitted values:
* `name`: Name assigned to the device.
* `device`: Device type. (rtp).
* `flavor`: Matterhorn "flavor" associated to the track. (presenter|presentation|other)
* `location`: Location of the RTSP URL to read from.
* `file`: The file name where the track will be recorded. (default: CAMERA.avi)
* `cameratype`: Video stream encoding type. (h264|mpeg4)
* `audio`: Whether the audio is captured. (True|False)
  * `audiotype`: Audio stream encoding type. (mp3|aac)
  * `vumeter`: Whether the audio input should be represented on the VU meter. (True|False)
  * `player`: Whether the audio input should be played on preview. (True|False)

Example:
```ini
[track1]
name = Axis
device = rtp
flavor = presenter
location = rtsp://127.0.0.1/mpeg4/media.amp
file = CAMERA.mp4
cameratype = mpeg4
audio = True
audiotype = mp3
vumeter = True
player = True
```
### Troubleshooting
**Asynchronism with no-RTP sources**

### FAQ
1. How can I locate the device?
1. Can the remote camera be outside my network?
1. Can I use a rtp URL?
