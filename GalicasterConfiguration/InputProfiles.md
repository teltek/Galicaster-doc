Input Profiles
==============

The page contains a general overview of the Input Profiles, including several downloadable examples. Please refer to the [Device module configuration](DeviceModuleConfiguration.md) section for a deeper explanation on how to configure a certain device.

### Input Profiles
Profiles are groups of tracks. Each track contains the reference to a device and its configuration.

**Profiles are ini files** located in directory `/etc/galicaster/profiles`

Each profile must have a name which identifies it on the Profile Selector. Additionally, a configuration script can be set up to run before the profile is loaded. These two values are defined in the data section, as shown below:

```ini
[data]
name = Profile  
execute = /home/user/script.sh  
```

#### Default profile
The *default profile* is the set of tracks defined directly in Galicaster's configuration file `conf-dist.ini`. Unlike the other profiles, it does not have a name and it is not defined in its own file within the `profiles` directory. Our recommendation is to leave the *default profile* as it is – two mock video sources and one mock audio source – and define all your profiles in their own files under the `profiles` directory.


### Device modules
A device module may accept several configuration parameters. Some are mandatory, but you may omit the rest of them and they will take their default value.
The **mandatory parameters** that are common to every plugin are:

* **device** - The plugin name to use with the device.
* **location** - The path to the device in the filesystem.
* **name** - A name to identify the device in the application.
* **file** - The file name and extension where the recorded data will be stored.
* **flavor** - A identifier representing the role of the track in the recording (*presenter*|*presentation*|*other*).

Certain device modules have mandatory values of their own. Please refer to the device *module* page to know them.

#### Tracks: Device module configuration
A *track* is the configuration of a single device through an appropriate Galicaster device module. A device can provide a video feed, an audio feed or both.
There are several types of device modules:

* Video plugin
  * [V4L2](DeviceModules/V4L2.md)
  * [Hauppauge](DeviceModules/Hauppauge.md) - audio available
  * [Epiphan](DeviceModules/Epiphan.md)
  * [Blackmagic](DeviceModules/Blackmagic.md) - audio available
  * [Firewire](DeviceModules/Firewire.md) - audio available on DV
  * [RTPvideo](DeviceModules/RTPvideo.md)
* Audio plugin
  * [Pulse](DeviceModules/Pulse.md)
* [Mock plugins](DeviceModules/Mock.md) - test plugins simulating a real device
  * Audiotest
  * Videotest
* Other:
  * Custom plugin

Find out which module is appropriate for your device by checking the [Device table](../HardwareRecommendations/CompatibleHardware.md).

#### Profile configuration
A Profile is build up of one or many tracks configuring several devices, usually from 1 to 4 (two videos and two audio streams). Profiles can be selected in the Profile Selector, by clicking on the button under "Recorder" in the welcome screen of Galicaster (only accessible in admin mode).

Profiles load automatically right after they are selected. If something goes wrong, an error message will be displayed on the Recorder area. Usually the error comes from an unplugged device or a misconfiguration. You may reload your profile again, after fixing the issue, by selecting it again in the Profile Selector.

Changing the current profile does not require to restart the application. However, make sure Galicaster is not running before editing your profile definitions.

### Encoding
Most device modules allow configuring its encoding and encapsulation. To know more about this matters please check out [Device module configuration](DeviceModuleConfiguration.md).

### Scripts and configuration commands
#### Logitech c920
Set the power line frequency to 60 Hz.
```bash
v4l2-ctl -d /dev/logitech --set-ctrl=power_line_frequency=2
```

#### Hauppauge PVR-350
Set the input to Svideo and the standard to PAL
```bash
v4l2-ctl -d /dev/hauppauge -i 1 -s 7
```

#### Profiles
As discussed earlier in this page, a profile is a set of tracks. Following are examples of the main tracks that Galicaster supports:

##### Logitech c920
```ini
[track1]
name = camera
device = v4l2
flavor = presenter
caps = video/x-raw,format=YUY2,framerate=24/1,width=1280,height=720
location = /dev/webcam
file = CAMERA.avi
```

##### Datapath VisionRGB-E1S
```ini
[track2]
name = camera
device = v4l2
flavor = presenter
caps = video/x-raw,format=YUY2,framerate=24/1,width=1024,height=768
location = /dev/screen
file = SCREEN.avi
```
For further information, please go to [Device Module Configuration](DeviceModuleConfiguration.md)

###### An complete example with mock devices:
```ini
[data]
name = Example

[track1]
name = Static
device = videotest
location = default
file = SCREEN.avi
flavor = presentation
caps = video/x-raw,framerate=25/1,width=640,height=480
pattern = 1
color1 = 4294967295
color2 = 4278190080

[track2]
name = Bars
device = videotest
flavor = presenter
location = default
file = CAMERA.avi
caps = video/x-raw,framerate=25/1,width=640,height=480
pattern = 0
color1 = 4294967295
color2 = 4278190080

[track3]
name = Noise
device = audiotest
location = default
file = sound.mp3
flavor = presenter
pattern = pink-noise
frequency = 440
volume = 0.3
player = True
vumeter = True
amplification = 1.0
```
On the example, the Static track will be displayed on the left and the Bars track on the right. The vu-meter will be connected to the Noise source.
