
Pulse device module
===================

*This page is updated to the 2.0.0 release*

This module records audio through the well-know PulseAudio sound server. It can capture audio coming from the various motherboard inputs and from USB audio devices.

Special features of this module are:
* Vu-meter
* Amplification and volume control

To capture this devices, additional configuring must be performed over the pulse layer through the Sound Settings or alsamixer.

### Pulse compatible devices
* [Revolabs wireless mics](Devices/Revolabs.md)
* Microphones (thr. motherboard)
* Audio mixers (thr motherboard)
* Build-in webcam microphones
* Osprey audio input


### Module Configuration

Admitted values:

* `name`: Name assigned to the device.
* `device`: Device type: pulse
* `flavor`: Matterhorn "flavor" associated to the track. (`presenter`|`presentation`|`other`)
* `location`: PulseAudio source name. Use default to select the same Input as the Sound Control
* `file`: The file name where the track will be recorded.
* `vumeter`: Activates data sending to the program's vumeter. (`True`|`False`) Only one device should be activated.
* `amplification`: Gstreamer amplification value: < 1 decreases and > 1 increases volume. Values between 1 and 2 are commonly used.
* `player`: Whether the audio will be previewed (played).

To list PulseAudio devices run:
```bash
$ pactl list | grep "Source" -A 5
```
and use "Name:" as the location field.

### Examples
```ini
[track3]
name = AudioSource
device = pulse
flavor = presenter
location = default
file = sound.mp3
active = True
vumeter = True
amplification = 2.0
channels = 2
delay = 0.0
```
