Compatible hardware
===================

*This page is updated to the 2.1 version*

In this section we will enumerate the devices and capture cards compatible with Galicaster, and mention the Galicaster modules designed to make them work. Usually, Galicaster captures a camera feed and a presentation feed from a laptop or similar device. Audio can be captured through the video capture card, through the soundcard or with specialized devices.

The devices included in the tables have been thoroughly tested and are being used by a growing community all over the world, so we recommend to use them preferably. Our participative community is a major reassurance on the hardware testing. However, other devices may work if they have Linux support at least. If you want to know if your Linux-supported device is compatible with Galicaster, please contact us and providing some information about the device.

Click on the **_Drivers & Info_** links for more information about the devices, instructions to install and configure the drivers, usual troubleshooting and frequently asked questions.

### Camera capture devices
Some card models by different vendors and for different video recording formats, from webcams to professional cameras, are included in the list below. Each device or capture card suits different scenarios and formats.

#### Recommended capture devices
| Device           |                | Model | GC Module | Connector | Signal | Format | Audio |
|------------------|----------------|-------|-----------|-----------|--------|--------|-------|
| Logitech webcams | [Drivers & Info](../GalicasterConfiguration/DeviceModules/Devices/Logitech.md) | c920, c910 BCC9500 | [v4l2](../GalicasterConfiguration/DeviceModules/V4L2.md) | USB | RAW | HD Full HD | Yes (pulse) |
| Blackmagic cards | [Drivers & Info](../GalicasterConfiguration/DeviceModules/Devices/Blackmagic.md) |	Decklink | [blackmagic](../GalicasterConfiguration/DeviceModules/Blackmagic.md) |	BNC or breakout cable | Multiple | SD-SDI and HD-SDI | Yes (embedded)|

#### Other capture devices
**_Not tested yet_**

| Device           |                | Model | GC Module | Connector | Signal | Format | Audio |
|------------------|----------------|-------|-----------|-----------|--------|--------|-------|
| Hauppauge cards  | [Drivers & Info](../GalicasterConfiguration/DeviceModules/Devices/Hauppauge.md) | PVR-350 PVR-250| [hauppauge](../GalicasterConfiguration/DeviceModules/Hauppauge.md) | RCA or 5-pin | SD | PAL/NTSC | Yes (raw and encoded) |
| Osprey cards     | [Drivers & Info](../GalicasterConfiguration/DeviceModules/Devices/Osprey.md) | 230 and others | [v4l2](../GalicasterConfiguration/DeviceModules/V4L2.md) | BNC and other (adaptors) | SD | PAL/NTSC pan. | Yes (pulse) |
| Axis cameras     | [Drivers & Info](../GalicasterConfiguration/DeviceModules/Devices/Axis.md) | multiple | [rtp](../GalicasterConfiguration/DeviceModules/RTP.md) | Ethernet | H264 or MPEG4 | up to QVGA | Some models only |
| Bluecherry cards | [Drivers & Info](../GalicasterConfiguration/DeviceModules/Devices/Bluecherry.md) | multiple | [v4l2](../GalicasterConfiguration/DeviceModules/V4L2.md) | BNC	 | SD | PAL/NTSC | Some models only |
| Firewire cameras | [Drivers & Info](../GalicasterConfiguration/DeviceModules/Devices/Firewire.md) | multiple | [firewire](../GalicasterConfiguration/DeviceModules/Firewire.md) | Firewire miniFW| SD or DV | PAL/NTSC | Some models only|

### VGA/DVI capture devices
Presentation is usually captured using specialized capture cards. Those cards can be connected to a variety of devices: PCs, laptops, tablets, projectors, VGA splitters and matrix switches. There are options to record VGA, DVI and HDMI sources.

#### Recommended VGA/DVI capture devices
| Device           |                | Model | GC Module | Connector | Signal | Format | Audio | Support Level|
|------------------|----------------|-------|-----------|-----------|--------|--------|-------|--------------|
| Datapath cards   | [Drivers & Info](../GalicasterConfiguration/DeviceModules/Devices/Datapath.md) | RGBVision 1es | [v4l2](../GalicasterConfiguration/DeviceModules/V4L2.md) | DVI | RGBHV |	upto QVGA | No | High |
| Blackmagic cards | [Drivers & Info](../GalicasterConfiguration/DeviceModules/Devices/Blackmagic.md) | Intensity | [blackmagic](../GalicasterConfiguration/DeviceModules/Blackmagic.md) | HDMI or breakout cable | Multiple | Full HD | Yes (embedded) | High |



#### Other VGA/DVI capture devices
**_Not tested yet_**

| Device                |                | Model | GC Module | Connector | Signal | Format | Audio | Support Level|
|-----------------------|----------------|-------|-----------|-----------|--------|--------|-------|--------------|
| Epiphan framegrabbers | [Drivers & Info](../GalicasterConfiguration/DeviceModules/Devices/Epiphan.md) | DVI2PCIe VGA2USB DVI2USB | [v4l2](../GalicasterConfiguration/DeviceModules/V4L2.md) | VGA or DVI | RGBHV |	upto QVGA | Not yet | Low |
| NCast | [Drivers & Info](../GalicasterConfiguration/DeviceModules/Devices/NCast.md) | Digitizer4 | [v4l2](../GalicasterConfiguration/DeviceModules/V4L2.md) | VGA | RGBHV | upto QVGA | No | None |

### Audio capture devices
Multiple devices may be used to capture audio, which can connect to the computer through the on-board sound card, a dedicated sound card or the USB ports. A external audio mixer is a good complement for audio capture, allowing multiple audio sources. Independent audio capture devices are recorded through the Pulse Audio system, thus sharing a common configuration.

#### Audio capture table
| Device |                | Model    | GC Module | Connector | Signal |
|--------|----------------|----------|-----------|-----------|--------|
|Line in | [Drivers & Info](../GalicasterConfiguration/DeviceModules/Devices/Revolabs.md) |	Multiple | [pulse](../GalicasterConfiguration/DeviceModules/Pulse.md)     | Line in   | Raw    |
