
Epiphan framegrabbers
=====================

**_NOT TESTED WITH GALICASTER 2.X_**  
*This page is updated to the 1.4.2 release*

#### Drivers & information
Epiphan framegrabbers are USB and PCI capture cards for VGA and DVI. The admit multiple resolution at different framerates.

* [Model table](#model-table)
* [Driver installation](#driver-installation)
* [Driver configuration](#driver-configuration)
* [VGA2USB and DVI2USB](#vga2usb-and-dvi2usb)
* [VGA2PCI and DVI2PCI](#vga2pci-and-dvi2pci)
* [Device identification](#device-identification)
* [Module configuration](#module-configuration)
* [Troubleshooting](#troubleshooting)
* [FAQ](#faq)

### Technical data
* Vendor: [Epiphan](http://www.epiphan.com/)
* Models **VGA2USB, VGA2PCI, DVI2USB, DVI2PCI and VGADVI Broadcaster** among others
* Resolution: **upto 1920×1200@60**
* Format: **RGB**
* Connector: **VGA or DVI**
* Signal: **RAW**
* Drivers: [available here](http://www.epiphan.com/downloads/linux/)
* GC Module: [epiphan](../Epiphan.md) or [rtp](../RTP.md) (Broadcaster)
* Price: **from 300 to 2000 $**


### Model table
| Model | Signal standards | Connectors | Audio | HD formats | SD Formats | HW Encoding | Price |
|-------|------------------|------------|-------|------------|------------|-------------|-------|
| [DVI2PCIe](http://www.epiphan.com/products/dvi-frame-grabbers/dvi2pcie/specifications/) | DVI VGA HDMI | DVI | None | 1080p 1920x1200 | 1600x1200, 1360x1024, 1400x1050, 1280x1024, 1280x960, 1280x800, 1152x900, 1152x864, 1360x768, 1024x768, 800x600, 640x480, 720x540, 720x480, 720x400 | No | 1000 $ |
| [DVI2USB](http://www.epiphan.com/products/dvi-frame-grabbers/dvi2usb/specifications/) | DVI | DVI | None | 1080p 1920x1200 (DVI) | 1600x1200, 1280x1024, 1280x960, 1152x900, 1152x864, 1024x768, 800x600, 640x480, 720x400 | No | 1000 $ |
| [VGA2USB](http://www.epiphan.com/products/frame-grabbers/vga2usb/specifications/) | VGA | VGA DE-15 | None | 1080p 1920x1200 | 1600x1200. 1280x1024, 1280x960, 1152x900, 1152x864, 1024x768, 800x600, 640x480, 720x400 | No | 300 $ |
| [VGA2USB LR](http://www.epiphan.com/products/frame-grabbers/vga2usb-lr/specifications/) | VGA | VGA DE-15 | None | None | 1280x1024, 1280x960, 1152x900, 1152x864, 1024x768, 800x600, 640x480, 720x400 | No | 800 $ |
| [VGA2USB HR](http://www.epiphan.com/products/frame-grabbers/vga2usb-hr/specifications/) | VGA | VGA DE-15 | None | 1080p | 1600x1200. 1280x1024, 1280x960, 1152x900, 1152x864, 1024x768, 800x600, 640x480, 720x400 | No | 1600 $ |
| [VGA2USB Pro](http://www.epiphan.com/products/frame-grabbers/vga2usb-pro/specifications/) | VGA | VGA DE-15 | None | 2048x2048, 2048x1546, 1920x1200 | 1600x1200. 1280x1024, 1280x960, 1152x900, 1152x864, 1024x768, 800x600, 640x480, 720x400 | No | 2000 $ |
| [VGADVI Broadcaster](http://www.epiphan.com/products/frame-grabbers/vga2usb-pro/specifications/) | DVI, VGA, HDMI, S-Video, Composite | DVI, S-Video | None | None | VESA modes 640x480 to 1920x1200 PAL, NTSC | H264, MPEG4 | 1600 $ |
Table information retrieved from:

* http://www.epiphan.com/products/frame-grabbers/  
Consult the specifications for supported HSync rates and framerate outputs.

### Driver installation
Download the drivers at http://www.epiphan.com/downloads/linux/index.php?dir=deb/

You should choose the driver according with some characteristics of your computer and operating system. Newer drivers are in the form of DEB packages .Run the following commands to retrieve the kernel release and architecture.

```bash
uname -rm
3.2.0-38-generic x86_64
```
To install the driver double-click in the DEB package. Ignore the error given by the Ubuntu Software Center. We recommend using the 3.27.7.25 version or upper.

### Driver configuration
To work with Epiphan USB and PCI based devices with Galicaster a certain configuration should be set that ensures a continuos stream, even on unplugging, and a fix resolution, with scaling activated.

Scaling options:

* 0: V2UScaleNone -No scaling
* 1: V2UScaleModeNearestNeighbor - Nearest neighbor algorithm
* 2: V2UScaleModeWeightedAverage - Weighted average algorithm
* 3: V2UScaleModeFastBilinear - Fast bilinear
* 4: V2UScaleModeBilinear - Bilinear
* 5: V2UScaleModeBicubic - Bicubic
* 6: V2UScaleModeExperimental - Experimental
* 7: V2UScaleModePoint - Nearest neighbour 2
* 8: V2UScaleModeArea - Weighted average
* 9: V2UScaleModeBicubLin - Luma bicubic, chroma bilinear
* 10: V2UScaleModeSinc - Sinc
* 11: V2UScaleModeLanczos - Lanczos
* 12: V2UScaleModeSpline - Natural bicubic spline

#### VGA2USB and DVI2USB
Minimum configuration:
```bash
echo options vga2usb v4l2_err_on_nosignal=0 > /etc/modprobe.d/epiphan.conf
```
Fix the resolution by adding the following lines with your target resolution to the previous file:
```bash
options vga2usb v4l_default_width=1280
options vga2usb v4l_default_height=720
options vga2usb v4l_nosig_img_width=1280
options vga2usb v4l_nosig_img_height=720
options vga2usb v4l_scalemode=4
```
Note: default and nossig resolutions must match.

Restart the computer to load the driver, or execute as root
```bash
modprobe vga2pci
```
#### VGA2PCI and DVI2PCI
Minimum configuration:
```bash
echo options vga2pci v4l2_err_on_nosignal=0 > /etc/modprobe.d/epiphan.conf
```
Fix the resolution by adding these lines to the previous file:
```bash
options vga2pci v4l_default_width=1280
options vga2pci v4l_default_height=720
options vga2pci v4l_nosig_img_width=1280
options vga2pci v4l_nosig_img_height=720
options vga2pci v4l_scalemode=4
```
Restart the computer to load the driver, or execute as root:
``` bash
modprobe vga2pci
```

### Device identification
1. Find the Device name attribute:
  * `udevadm info --attribute-walk --name=/dev/video0 | grep name`
    * Usual Device IDs:
        * *vga2usb*, *vga2pci*, *dvi2pci*
1. Fix access path
  * With sudo create or modify the file `/etc/udev/rules.d/galicaster.rules`
  * Add the line: ```KERNEL=="video[0-9]*", ATTR{name}=="DVI2PCIe", GROUP="video", SYMLINK+="epiphan"```

### Module configuration
##### Admitted values
* `name`: Name assigned to the device.
* `device`: Device type: epiphan
* `flavor`: Matterhorn "flavor" associated to the track. (**presenter**|*presentation*|*other*)
* `location`: Device's mount point in the system (e.g. `/dev/screen`).
* `file`: The file name where the track will be recorded. (default:`CAMERA.avi`)
* `drivertype`: Wheter the device use a v4l or a v4l2 interface to guarantee compatibility (v4l|**v4l2**)
  * As for Ubuntu 10.10 use v4l. Otherwise v4l2 (default value)
* `resolultion`:Output resolution
* `framerate`: Output framerate  
*PENDING: more info on framerate and resolution

##### Example:
```ini
[track2]
name = Epiphan
device = epiphan
flavor = presentation
location = /dev/screen
file = SCREEN.avi
active = True
drivertype = v4l2
resolution = 1024,768
framerate = 30/1
```

### Troubleshooting
**Incompatibility with Blackmagic capture cards**  
Due to a conflict between the drivers of Blackmagic and Epiphan cards drivers, their devices are incompatible one to the other. Combinations of these devices with ones or other vendor others has been succesfully tested.

**Problems with resolution change**  
If you expirience problems with resolution changes please make sure all the parameters on the driver configurartion match the syntax. Resolutions should be scaled to the default resolution defined. Also, check your driver version, drivers older than 3.27.7.5 may present scaling problems.

**Panoramic resolution scaling**  
Panoramic resolution aspect won't be respected when default resolution is 4:3. To use panoramic resoultion better use a panoramic default resolution. When combining 4:3 and 16:9 and other ratios introduce auxiliary hardware such as VGA scalers.

### FAQ
