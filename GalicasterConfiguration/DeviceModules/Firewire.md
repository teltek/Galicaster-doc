
Firewire device module
======================

**NOT TESTED WITH GALICASTER 2**
**THIS PAGE IS UNDER CONSTRUCTION**

The Firewire device module is meant to give compatibility for Firewire video cards working with DV or miniDV professional cameras.

### Firewire compatible devices
* [Firewire cards and any DV or mini-DV camera](Devices/Firewire.md)

### Module Configuration
Admmited values:

* `name`: Name assigned to the device.
* `device`: Device type: blackmagic
* `flavor`: Matterhorn "flavor" associated to the track. (`presenter`|`presentation`|`other`)
* `location`: Device's mount point in the system (e.g. `/dev/video0`).
* `file`: The file name where the track will be recorded.
* `format`: Input signal format. (`dv`|`hdv`|`iidc`)
* `vumeter`: Activates data sending to the program's vumeter. (`True`|`False`) Only one device should be activated.
* `player`: Whether the audio input would be played on preview. (`True`|`False`)

### Examples
```ini
[track1]
name = Firewire
device = firewire
flavor = presenter
location = /dev/fw0
file = CAMERA.dv
format = dv
vumeter = True
player = True
```
