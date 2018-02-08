
Blackmagic device module
========================

*This page is updated to the 2.1 version*

The blackmagic device module provides compatibility with those Blackmagic Design capture cards compatible with Linux, for instance Decklink SDI and Intensity Pro. These capture cards are focused on recording High Definition formats but they also record other formats such as Svideo, Composite and Components.

Consult our page dedicated to [Blackmagic cards](../../HardwareRecommendations/BlackmagicCards.md) for a more detailed information.

### Blackmagic Linux-compatible cards
* [Blackmagic Intensity Series](Devices/Blackmagic.md)
* [Blackmagic Decklink Series](Devices/Blackmagic.md)


### Technical details
#### Blackmagic Decklink SDI
From http://www.blackmagicdesign.com/products/decklink/techspecs

| Connectors | SD Formats | HD Formats 720p | HD Formats 1080i | HD Formats 180p | Audio Input |
|------------|------------|------------|------------|------------|------------|
| BNC and Breakout cable	|625/25 PAL, 525/29.97 NTSC and 525/23.98 NTSC| 720p50, 720p59.94, 720p60 | 1080i50, 1080i59.94 and 1080i60 | 1080PsF23.98, 1080p23.98, 1080PsF24, 1080p24, 1080PsF25, 1080p25, 1080PsF29.97, 1080p29.97, 1080PsF30, 1080p30 | 8 Channels embedded in SD and HD |


#### Blackmagic Intensity PRO (HDMI)
http://www.blackmagicdesign.com/products/intensity/

| Connectors | SD Formats | HD Formats 720p | HD Formats 1080i | HD Formats 180p | Audio Input |
|------------|------------|------------|------------|------------|------------|
| HDMI 4:2:2 and Breakout cable with components (also composite and svideo | 625i/50 PAL and 525i/59.94 NTSC. | 720p50, 720p59.94 and 720p60 | 1080i50, 1080i59.94 and 1080i60 | 1080p23.98, 1080p24, 1080p25, 1080p29.97 and 1080p30 | 2 Channel RCA HiFi audio in 24 bit | Estereo RCA, HDMI embeded |

#### Module Configuration

##### Admitted values:

* `name`: Name assigned to the device.
* `device`: Device type: blackmagic
* `location`: Device's mount point in the system.
* `file`: The file name where the track will be recorded.
* `flavor`: Matterhorn "flavor" associated to the track. (`presenter`|`presentation`|`other`)
* `input`: Input signal format. (`sdi`|`hdmi`|`opticalsdi`|`component`|`composite`|`svideo`)
* `input-mode`: Input video mode and framerate (eg. 1080i60). More information here.
* `audio-input`: Input audio mode (`none`|`auto`|`embedded`|`aes`|`analog`). More information here.
* `subdevice`: Select a Blackmagic card from a maximum of 4 devices (0-3, Default: 0)
* `audio-input`: Input audio mode (`none`|`auto`|`embedded`|`aes`|`analog`). More information here.
* `vumeter`: Activates data sending to the program's vumeter. (`True`|`False`) Only one device should be activated.
* `player`: Whether the audio input would be played on preview. (`True`|`False`)
* `amplification`: Gstreamer amplification value: < 1 decreases and > 1 increases volume. Values between 1 and 2 are commonly used. (0-10)

#### Examples
##### Decklink with SDI and audio automatic
```ini
[track1]
name = Decklink
device = blackmagic
flavor = presenter
file = CAMERA.avi
location = /dev/blackmagic0
input = sdi
input-mode = 720p50
audio-mode = auto
subdevice = 0
vumeter = True
player = False
amplification = 1.0
```
##### HDMI at 1080p 50 fps without audio
```ini
[track2]
name = BlackmagicHDMI
device = blackmagic
location = /dev/blackmagic1
file = CAMERA.avi
flavor = presentation
input = hdmi
input-mode = 1080p50
audio-mode = none
subdevice = 0
```
