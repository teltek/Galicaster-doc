Device module configuration
===========================

*This page is updated to the 2.1 version*

The configuration of a capture card or device involves different aspects:

* Driver installation - explained on each device page
* Driver and device configuration - static and dynamic configuration made through `modprobe`, `v4l2-ctl` and similar commands.
* Device module configuration - setup the Galicaster adaptation modules for each device

Each device family has its own page with information, including driver-related instructions. These pages are listed at the [Compatible hardware](../HardwareRecommendations/CompatibleHardware.md).

This section will focus on the device module configuration. Every device or capture card is handled with a specific device module depending on their nature. After you read this page check the links on the following list for more information about a specific modules:

* [V4l2 device module](DeviceModules/V4L2.md) (Datapath, Epiphan and other devices)
* [Blackmagic device module](DeviceModules/Blackmagic.md)
* [Pulse device module](DeviceModules/Pulse.md)
* [NDI device module](DeviceModules/NDI.md)
* [Hauppauge device module](DeviceModules/Hauppauge.md) (*Not tested with Galicaster 2*)
* [Firewire device module](DeviceModules/Firewire.md) (*Not tested with Galicaster 2*)
* [RTP device module](DeviceModules/RTP.md) (*Not tested with Galicaster 2*)

### Common parameters
The device module configuration sets the parameters necessary to capture, preview and process the incoming data from a device or capture card. Every device module has 6 common parameters:

* `name`: Name assigned to the device.
* `device`: Device module type.
* `file`: Filename - not route - where the data will be stored, including the extension.
* `location`: Device mount point on the filesystem (source of the data coming from the device).
* `flavor`: The role the device plays in the recording.
* `tags`: Optional array of 'tags' to be added to the device track.

### Audio parameters
The device modules with audio capturing capabilities have the ability to amplify and preview audio. Preview is done by playing the audio live and/or displaying its level in a VU meter. The parameters related to the audio preview are:

* `vumeter`: Whether this audio input will be represented on the vumeter. (True|False)
* `player`: Whether this audio input will play on the preview. (True|False)
* `amplification`: Sound amplification value. A value lower than 1 decreases volume, and greater than 1 increases it. Values between 0.0 and 2.0 are commonly used. The amplification is made by software, using GStreamer.
  * *Sources that produce an encoded output - hauppauge, firewire - will NOT amplify the audio level*.

### Encoding paramaters
Depending on its nature, a device module may allow to configure its encoding and formatting parameters. These parameters expect the name of a Gstreamer component, or a series of linked components specified using the usual Gstreamer syntax. You may choose among the whole set of Gstreamer encoders and muxers.

* `videoencoder`: Encoder element and filters for video encoding.
* `audioencoder`:Encoder element and filters for audio encoding.
  * Audio-only sources should include the audio muxer, if needed, into this parameter.
* `muxer`: Muxing element for video and/or audio encapsulation
  * Please note that only some encoder-muxer combinations are possible. Galicaster will not check whether the syntax or the combination of elements are valid, so invalid configurations may produce errors.

Some device modules do not handle encoding parameters, partially or totally:

* Hauppauge cards encode mpeg2-mpegts via hardware. Alternatively, they may be used with a `v4l2` device module, so that the encoding parameters can be set up as any other v4l2 device.
* Firewire encodes to dv-dv or dv-avi (the lattest experimental).
* Rtp encodes to mpeg4 or h264, the muxer is configurable.

#### Examples:
Find out more about the each element's valid parameters using the GStreamer inspect command:

```bash
gst-inspect-1.0 <element>
```

##### h264, MP3 and AVI (Recommended)
```ini
videoencoder = x264enc pass=5 quantizer=22 speed-preset=4 profile=1
audioencoder = lamemp3enc target=1 bitrate=192 cbr=true
muxer = avimux
```

##### Xvid, MP3 and AVI
```ini
videoencoder = xvid bitrate=5000000
audioencoder = lamemp3enc target=1 bitrate=192 cbr=true
muxer: avimux
```

##### MPEG2, AAC and MPEG4
```ini
videoencoder: ffenc_mpeg2video quantizer=4 gop-size=1 bitrate=10000000
audioencoder: voaacenc bitrate=96000 profile=3
muxer: mp4mux
```

##### Theora- Vorbis - Ogg
```ini
videoencoder = theoraenc bitrate=5000
audioencoder = vorbisenc
muxer = oggmux
```
