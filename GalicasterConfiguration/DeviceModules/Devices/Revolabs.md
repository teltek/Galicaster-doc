Revolabs wireless microphones
=============================

**THIS PAGE IS UNDER CONSTRUCTION**

### Drivers & information
Revolabs wireless microphones are devices well adapted to a classroom or conference environment. It consists in two pieces: a bay and the microphone.
The bay is connected to the computer to send the audio and it also works as battery recharder.
The microphone is cilindric with a structure for attaching it to the clothing. The cilinder incorporates two microphones, one for speech recording and a second one to receive the room noise to process the signal and improve the audio quality.o

* [Driver installation](#driver-installation)
* [Device identification](#device-identification)
* [Device configuration](#device-configuration)
* [Plugin configuration](#plugin-configuration)
* [Use instructions](#use-instructions)
  * [Charging the Batteries](#charging-the-batteries)
  * [Pairing the microphone to the base](#pairing-the-microphone-to-the-base)
* [Troubleshooting](#troubleshooting)
* [FAQ](#faq)

### Technical data
* Vendor: [Revolabs](http://www.revolabs.com/)
* Models **solo, xTag**
* Format: **PCM**
* Connector: **USB or Line in**
* Signal: **RAW**
* Drivers: **pre-installed on Ubuntu 12**
* Plugin: [pulse](../Pulse.md)
* Price: **600 €** (microphone and bay)

### Driver installation
The driver is included in the linux kernel.

Back to top
### Device identification
1. Find the Device name attribute:
  * `pactl list | grep Source -A 3`
  * alsa_input.usb-revolabs_solo-Desktop-00-soloDesktop.analog-mono

### Device configuration
Use alsamixer or Sound Settings to unmute, configure and amplify the device.

*PENDING: pair with base and charge behaviour.


### Plugin configuration
#### Admitted values:
* `name`: Name assigned to the device.
* `device`: Device type: pulse
* `flavor`: Matterhorn "flavor" associated to the track. (`presenter`|`presentation`|`other`)
* `location`: PulseAudio source name. Use default to select the same Input as the Sound Control
* `file`: The file name where the track will be recorded.
* `vumeter`: Activates data sending to the program's vumeter. (`True`|`False`) Only one device should be activated.
* `amplification`: Gstreamer amplification value: < 1 decreases and > 1 increases volume. Values between 1 and 2 are commonly used.
* `player`: Wheter the audio will be previewed (played).

* to list PulseAudio devices run: ``$ pactl list | grep "Source" -A 3`  
and use "Name:" as the location field.

#### Example:
```ini
[track1]

name = AudioSource
device = pulse
flavor = presenter
location = alsa_input.usb-revolabs_solo-Desktop-00-soloDesktop.analog-mono
file = sound.mp3
vumeter = True
amplification = 2.0
```
### Use instructions
#### Charging the Batteries
To charge the batteries place the Microphone into the xTag Charger Base. During charging, the Microphone status LED indicator
changes from solid RED to solid GREEN as chargingcompletes. The Charger Base status indicator remains off during charging. The Microphone is always muted while in the Charger Base. **  The battery charges from fully depleted to fully charged in approximately two hours, however,** it is “quick-charged” to **80% capacityin 45 minutes.**  
_Note: A fully charged battery provides approximately 8 hours of talk time._

*When to Charge*
When the Microphone LED begins flashing alternating YELLOW and RED or YELLOW and GREEN, the battery needs recharging.

#### Pairing the microphone to the base
“Pairing” creates an encrypted association between the Wireless Microphone and the Charger Base with a unique electronic serial number. Once the Microphone and Charger Base have been paired, the Microphone will automatically try to connect to the Charger Base whenever it is lifted from the Charger Base. Remember, the Microphone is always muted (flashing RED LED) when it is first removed from the Charger Base and the MUTE button needs to be pressed to activate the Microphone, as indicated by a flashing GREEN LED.

If a Microphone is lifted from the Charger Base and the Microphone LED slowly flashes alternating RED and GREEN for 10 seconds, it means that the Microphone needs to be paired to the system. To pair the Microphone to the Charger Base:
* Make sure the Microphone is turned OFF (no LED activity). If the unit is ON, press and hold the MUTE button for 10 seconds until the LED turns
solid RED then release. Alternately, place the Microphone in the Charger Base for less than 2 seconds.
* Enable the pairing mode by holding the Microphone’s Mute button down for eight seconds. The LED will turn solid GREEN and then solid
RED. Release the Mute button. The Microphone unit is now in pairing mode.
* Push and hold the Charger Base’s Mute button for eight seconds to enter into pairing mode then release. The LED will be solid RED until pairing is
complete, as indicated by double flashing RED on both the Microphone and the Charger Base (paired and muted audio). If pairing fails at the end of one
minute on either unit, the LED will flash alternately GREEN and RED for a few seconds and turn OFF. If this happens, repeat these steps.

### Troubleshooting
**Charge**  
A Revolabs microphone with a new battery last about 8 hours. It has a quick charge to 80% of 45 minutes and then to 100% on 2 hours.

### FAQ
