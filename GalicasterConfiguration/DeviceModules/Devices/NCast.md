
NCast digitizer cards
=====================

**_NOT TESTED WITH GALICASTER 2.X_**  
*This page is updated to the 1.4.2 release*

### Drivers & information
NCast Digitizer capture cards are able to detect input automatically, supporting many resolutions up to 1920x1200. They are also able to capture two video streams simultaneously, creating a side-by-side composite stream by hardware.

* [Driver installation](#driver-installation)
* [Device identification](#device-identification)
* [Device configuration](#device-configuration)
* [Module configuration](#module-configuration)

### Technical data
* Vendor: [NCast](http://www.ncast.com/)
* Models [Digitizer](http://www.ncast.com/pdf/NCast-UG-DigitizerCard2.pdf)
* Resolution: from 640x350 to 1920x1200
* Connector: **dual** (BNC and DVI-A)
* Signal: RAW
* Drivers: [latest](http://www.ncast.com/files/digitizer4-2_3_1_5.tgz)
* Plugin: [v4l2](../V4L2.md)
* Price: **around 100 €**


### Driver installation
To download and install the driver run:
```bash
wget http://www.ncast.com/files/digitizer4-2_3_1_5.tgz
tar xvf digitizer4-2_3_1_5.tgz
cd digitizer4/
make
make install
sudo modprobe digitizer4
```

A full guide to install and configure the driver is already included in the package, in the file named `README`.

### Device identification
Find the Device name attribute:
```bash
udevadm info --attribute-walk --name=/dev/video0 | grep name
```

### Device configuration
NCast Digitizer cards are configured by issuing textual parameters to the device at /proc/digitizer using the echo command.

#### Parameters

* Set Main input: set_vga, set_dvi, set_composite, set_svideo, set_auto. Example:
echo "set_vga" > /proc/digitizer
* Set Picture-in-picture input: set_pip_vga, set_pip_dvi, set_pip_composite, set_pip_svideo, set_pip_auto, set_pip_on, set_pip_off, swap_main_pip.
* Set window size:
  * set_window X[%] Y[%] WIDTH[%] HEIGHT[%]
  * set_pip_window X[%] Y[%] WIDTH[%] HEIGHT[%]
* Example:
```bash
echo "set_window 0% 0% 100% 100%" > /proc/digitizer
```

Please check the README file in the driver's package for further information and the full list of available parameters.

Module configuration
#### Admitted values

| Property name | Description | Accepted values | Default |
|---------------|-------------|-----------------|---------|
| `name` | Name assigned to the device | Free text ||
| `device` | Device type | v4l2 | `v4l2` |
| `flavor` | Matterhorn "flavor" associated to the track | presenter, presentation, other | `presenter` |
| `location` | Device mount point in the system | /dev/video0, /dev/webcam), etc... ||
| `file` | The file name where the track will be recorded | Any valid file name | `CAMERA.avi` |
| `videocrop-top`<br>`videocrop-bottom`<br>`videocrop-left`<br>`videocrop-right` | Indicates the number of pixels to be removed from the corresponding side of the picture. It may be used to adjust the aspect ratio, e.g. get a 4:3 output from a 16:9 video. Optional. | Integer ||

* `name`: Name assigned to the device.
* `device`: Device type. (**v4l2**)
* `flavor`: Matterhorn "flavor" associated to the track. (**presenter**|presentation|other)
* `location`: Device's mount point in the system (e.g. /dev/video0 or /dev/webcam).
* `file`: The file name where the track will be recorded. (default: CAMERA.avi)
* `videocrop-top`  
  videocrop-bottom  
  videocrop-left  
  videocrop-right (optional): Number of pixels to be removed from the corresponding side of the picture. It may be used to get a 4:3 aspect ratio out of a 16:9 video.
* `caps`: GStreamer capabilities of the device (mimetype=TYPE, framerate=X/Y,width=A,height=B)

#### Caps magic
* type: **video/x-raw**
  * image/jpeg usually provides better framerate-resolution ratio, leaving de transcoding to the software
* framerate: `24/1`, `25/1` or `30/1` for full motion; `10/1` or `15/1` for testing.
* resolution:
  * `width=800,height=600`, `width=640,height=480`, `width=1024,height=768`
  * panoramic: `width=1280,height=720` - `width=1920,height=1080`
* Use `guvcview` to know wich capabilities are compatible with your device.

More information at http://pygstdocs.berlios.de/pygst-tutorial/capabilities.html

#### Example
```ini
[track1]
name = NCast
device = v4l2
flavor = presentation
location = /dev/ncast
file = SCREEN.avi
```
