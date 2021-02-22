
NDI device module
==================

*This page is updated to the 2.1 version*

NDI module provides compatibility with NewTek NDI streaming protocol. It can record multiple video streams with our without audio. Or only record audio from a stream.

### Module configuration
Admitted values:

* `name`: Name assigned to the device.
* `device`: Device type: (`ndi`|`ndi_audio` )
* `flavor`: Matterhorn "flavor" associated to the track. (`presenter`|`presentation`|`other`)
* `location`: URL or Stream Name to the NDI source (e.g. `GC-DEV (OBS)` or `10.21.10.22:5961`).
* `file`: The file name where the track will be recorded. (The path is automatically assembled)
* `audio`: Whether the audio is recorded or not. (`True`|`False`). **Use only with device `ndi`**
* `vumeter`: Activates data sending to the program's vumeter. (`True`|`False`) Only one device should be activated. **Use only with device `ndi_audio`**
* `amplification`: Gstreamer amplification value: < 1 decreases and > 1 increases volume. Values between 1 and 2 are commonly used. **Use only with device `ndi_audio`**
* `player`: Whether the audio will be previewed (played). **Use only with device `ndi_audio`**

### Examples:
##### NDI video stream with audio
```ini
[track1]
name = OBS NDI
device = ndi
location = GC-DEV (OBS)
file = WEBCAM.avi
flavor = presenter
audio = True
```
Also it's possible to only record audio from a NDI stream
##### NDI stream only with audio
```ini
[track1]
name = NDI Audio
device = ndi_audio
location = GC-DEV (OBS)
file = sound.mp3
flavor = presenter
player = True
vumeter = True
amplification = 1.0
```
