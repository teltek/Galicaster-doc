Firewire-based professional cameras
===================================

**_NOT TESTED WITH GALICASTER 2.X_**  
*This page is updated to the 1.4.2 release*

### Drivers & information
Firewire-based professional cameras recording in Digital Video (DV) are compatible with Galicaster. Cameras with a DV or miniDV output may also be used through a Linux-compatible firewire interface.

* [Driver installation](#driver-installation)
* [Device identification](#device-identification)
* [Device configuration](#device-configuration)
* [Module configuration](#module-configuration)
* [Troubleshooting](#troubleshooting)
* [FAQ](#faq)

#### Technical data
* Vendor: **Multiple**
* Resolution: **PAL/NTSC**
* Format: **DV**
* Connector: **Firewire**
* Signal: **RAW**
* Drivers: **pre-installed on Ubuntu 12**
* Plugin: [firewire](../Firewire.md)


### Driver installation
The driver is included in the Linux kernel – `firewire-core and firewire-ohci`.

### Device identification
1. Find the Device name attribute:
```bash
udevadm info --attribute-walk --name=/dev/fw0 | grep name
```

### Device configuration

### Module configuration
#### Admitted values:
* `name`: Name assigned to the device.
* `device`: Device type. (**firewire**)
* `flavor`: Matterhorn "flavor" associated to the track. (**presenter**|presentation|other)
* `location`: Device mount point in the system. (e.g. `/dev/video0 or /dev/webcam`).
* `file`: The file name where the track will be recorded. (default: CAMERA.**avi**)
* `vumeter`: Whether the audio input should be represented on the VU meter. (True|False)
  * **Note:** This parameter should be set in only one device at a time.
* `player`: Whether the audio input should be played on preview.
* `format`: Input DV video format. (**dv**|hdv|iidc)

Example:
```ini
[track1]
name = Camera
device = firewire
flavor = presenter
location = /dev/fw0
file = CAMERA.dv
vumeter = True
player= True
format = dv
```
### Troubleshooting

### FAQ
