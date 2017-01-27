
RTP device module
=================

**THIS PAGE IS UNDER CONSTRUCTION**

The Rtp device module is focused on Network-based Cameras with hardware encoding. This module records the RTP stream directly, whether it is is encoded on MPEG4 or H264, and decodes it for visualization. It can record streams with our without audio.

Rtp has been tested with several [Axis Network cameras](Devices/Axis.md) of both MPEG4 and H264 encoding, and with the Epiphan VGADCI Broadcast.

### RTP compatible devices
* [Axis Network cameras](Devices/Axis.md)
* Epiphan Broadcast

### Module Configuration
##### Admitted values:

* `name`: Name assigned to the device.
* `device`: Device type: rtp
* `flavor`: Matterhorn "flavor" associated to the track. (`presenter`|`presentation`|`other)`
* `location`: URL to the RTP source. (e.g. `rtsp://127.0.0.1:554/mpeg4`).
* `file`: The file name where the track will be recorded.
* `cameratype`: Whether the device streams a MPEG4 or H264 stream. (`mpeg4`|`h264`)
* `audio`: Whether the audio is recorded or not. (`True`|`False`)
* `audiotype`: Audio format to capture, by default mp3. (`acc`|`mp3`)
* `videomux`: Muxer to encapsulate the stream. FLV by default, other options include `mpegtsmux`, `avimux`, `mp4mux`.

### Examples
##### MPEG4 without audio
```ini
[track1]
name = AXIS 212PTZ
device = rtp
location = rtsp://127.0.0.1:554/mpeg4/media.amp
file = CAMERA.mpeg.ts
flavor = presenter
cameratype = mpeg4
audio = False
videomux = mpegtsmux
```

##### H264 with audio
```ini
[track1]
name = AXIS Q7404
device = rtp
location = rtsp://127.0.0.1:554/axis-media/media.amp?videocodec=h264
file = CAMERA.flv
flavor = presenter
cameratype = h264
audio = True
audiotype=mp3
```
