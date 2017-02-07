
Logitech webcams
================

### Drivers & information
Logitech HD Webcams are compatible with Galicaster. They provide HD and Full HD videos. Other Logitech UVC webcams will work but most of them don't provide a fair resolution-framerate ratio.

* [Driver installation](#driver-installation)
* [Device identification](#device-identification)
* [Device configuration](#device-configuration)
* [Module configuration](#module-configuration)
* [Troubleshooting](#troubleshooting)
* [FAQ](#faq)

#### Technical data
* Vendor: [Logitech](http://www.logitech.com/en-us/home)
* Models [c920](http://www.logitech.com/en-us/product/hd-pro-webcam-c920) and [BCC950](http://www.logitech.com/en-us/product/Conferencecam?crid=1252)
* Resolution: **upto Full HD**
* Format: **YUV or JPEG**
* Connector: **USB 2.0**
* Signal: **RAW**
* Drivers: **pre-installed on Ubuntu 12**
* Plugin: [v4l2](../V4L2.md)
* Price: **around 100 €**


### Driver installation
The driver is included in the linux kernel - uvcvideo.

### Device identification
1. Find the Device name attribute:
  * `udevadm info --attribute-walk --name=/dev/video0 | grep name`
    * Usual Device IDs:
      * Logitehc c920 on Ubuntu 12.04: HD Pro Webcam C920
      * Logitehc c910 on Ubuntu 12.04: HD Pro Webcam C910
      * Logitehc c910 on Ubuntu 10.10: UVC Camera (046d:0821)

2. Fix access path
  * Create or modify the file `/etc/udev/rules.d/galicaster.rules.`
  * Add the line: `KERNEL=="video[0-9]*", ATTR{name}=="HD Pro Webcam C920", GROUP="video", SYMLINK+="logitech"`

### Device configuration
To probe the possible parameteres we recommend using **guvcview**, which will show the possible values to each parameter.
Later, to fix the parameters use the video4linux2 CLI configuration and compound your configuration on a script:

To list the parameters:

* `v4l2-ctl -d /dev/video0 -L`

Useful commands

  * Powerline frequency: `v4l2-ctl -d /dev/logitech -c power_line_frequency=1` (1: 50 Hz 2: 60 Hz)
  * Autofocus:
  * Exposure: `v4l2-ctl -d /dev/logitech -c exposure_auto=0` (0:auto, 1:manual, 2:shutter, 3:aperture)

### Module configuration
#### Admitted values:
* `name`: Name assigned to the device.
* `device`: Device type: v4l2
* `flavor`: Matterhorn "flavor" associated to the track. (`presenter`|`presentation`|`other`)
* `location`: Device's mount point in the system (e.g. `/dev/video0 or /dev/logitech`).
* `file`: The file name where the track will be recorded. (default:`CAMERA.avi`)
* `videocrop`: Margin in pixels to be cutted. Useful to set a 4:3 proportion on a HD webcam.videocrop-top, videocrop-bottom, videocrop-left, videocrop-right. (optional)
* `caps`: GStreamer cappabilities of the device (`mimetype=TYPE, framerate=X/Y,width=A,height=B`)

#### Caps magic:
* type: (**image/jpeg** | video/x-raw)
  * image/jpeg usually provides better framerate-resolution ratio, leaving de transcoding to the software
* framerate: 24/1,25/1 or 30/1 for full motion 10/1 15/1 for testing.
* resolution:
  * width=800,height=600, width=640,height=480, width=1024,height=768
  * panorarmic: width=1280,height=720 - width=1920,height=1080
* Use **guvcview** to know wich capabilities are compatible with your device.

#### Example:
```ini
[track1]
name = Webcam
device = v4l2
flavor = presenter
location = /dev/logitech
file = WEBCAM.avi
caps = image/jpeg,framerate=24/1,width=1280,height=720
videocrop-left = 160
videocrop-right = 160
```

### Troubleshooting
**USB Amplifiers**  
USB amplifiers should be extended. Spirals along the wire will cause inductancy and thus damaging the signal
Also, some USB extensors have been reported to fail occasionally.

### FAQ
1. Why is the preview jumpy?
  * The application may drop frames if is not capable of preview them fast enough. If the recording is jumpy too your computer may be not powerful enough capturing the video at the current framerate and resolution. Try lower parameters and close any other application that may affect CPU performance.
1. Why is image is blurry?
  * This devices usually have autofocus cappabalities, set a custom focus and disable the autofocus.
1. If I disconnect the webcam, will I lost the recording?
  * Most certainly, the system is very sensitive with USB devices so during a recording the device must remain plugged.
1. I'm using an USB extensor but I'm getting errors.
  * USB wires can transmit information without losses up to 3 meters. To reach a longer distance you need a wire with an amplifier. There are amplified chords up to 20 meters. These chords should be fully extended, since inductancy can affect the signal.
