
Epiphan device module
=====================

**_NOT TESTED WITH GALICASTER 2.X_**  
*This page is updated to the 1.4.2 release*

Epiphan framegrabbers are able to record VGA, DVI and HDMI inputs. They are meant to record from an computer, laptop, projectors or other devices using RGB format.

This module is meant to adapt to those Epiphan framegrabbers compatible with V42L. It's special features are:

* Provide a continuous input in case the device is unplugged accidentally.
* Define a output resolution to which scale the unknown incoming stream.
* Ensure or limit the framerate.

For Epiphan VGADVI Broadcaster use the [RTP device module](RTP.md)

### Epiphan compatible devices
* [Epiphan framegrabbers](Devices/Epiphan.md)
  * Epiphan DVI2PCI2
  * Epiphan DVI2USB
  * Epiphan VGA2USB (LR, HR and Pro)
  * Epiphan VGA2PCI - obsolete, replaced by DVI2PCIe

### Module Configuration
Admitted values:
* `name`: Name assigned to the device.
* `device`: Device type: vga2usb
* `flavor`: Matterhorn "flavor" associated to the track. (`presenter`|`presentation`|`other`)
* `location`: Device's mount point in the system (e.g. `/dev/video0`).
* `file`: The file name where the track will be recorded.
* `drivertype`: Whether the device use a v4l2 or a v4l interface, to guarantee backwards compatibility (`v4l2`|`v4l`)
As for Ubuntu 10.10 or similar use `v4l`.
* `resolution`: Output resolution. If the input resolution doesn't match the output, the input will be scaled respecting the ratio - by introducing black borders.
* `framerate`: Output framarate. If the input framerate doesn't match the output, frames will be dropped or duplicated accordingly.

### Examples
```ini
[track1]
name = DVI2PCIe
device = epiphan
flavor = presentation
location = /dev/screen
file = SCREEN.avi
resolution = 1024,768
framerate = 10/1
drivertype = v4l2
```
