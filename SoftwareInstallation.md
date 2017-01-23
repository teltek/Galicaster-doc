Software installation
=====================

*This page is updated to the 1.4.2 release*

Installation process
--------------------
The installation process consists of 5 simple steps:

* [Check the prerequisites.](#prerequisites)
* [Download the latest Galicaster version.](#download)
* [Install the software.](#installation)
* [Run Galicaster for the first time.](#run-galicaster-for-the-first-time)
* [Install and configure drivers.](#install-drivers)

After installing, the next step is configuring the system.
Advanced users, or those with special needs, can download the [source code](https://github.com/teltek/Galicaster) and make a manual installation.

### Prerequisites
Before starting the installation process, please make sure that:

* If you already have a Galicaster running in your computer, please refer to the [upgrade](SoftwareInstallation/UpgradingFromOlderVersions.md) documentation.
* Your equipment meets Galicaster [Hardware Recommendations.](HardwareRecommendations.md)
* You are running a Linux-based OS. The recommended distribution is Ubuntu 12.04. Make sure that the version chosen matches your system architecture (32 or 64 bits). We also recommend the distribution [Ubuntu 12.04.5](http://releases.ubuntu.com/12.04/) since it has the kernel 3.13.0 included. In case of using previous versions (like 12.04.1) you may have to install the next packages:

```bash
apt-get -y install xserver-xorg-lts-trusty
apt-get -y install linux-generic-lts-trusty
```

### Download
The latest Galicaster version can be downloaded [here](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.4.1_all.deb), as a DEB package. Older versions and information about the new features that each of them included are available on the [Release Archive.]()

By downloading, you agree to the [non-commercial license](http://creativecommons.org/licenses/by-nc-sa/3.0/). (Commercial licenses also available under request) ￼![](http://i.creativecommons.org/l/by-nc-sa/3.0/80x15.png)

#### Source code
As an alternative to the DEB package installation, you can install Galicaster from the source code. Stable versions are available on the [Release archive](). Stable and development versions, as well as development information, are available in our [Git repository](http://github.com/teltek/Galicaster).

Installing a source code version requires installing its [dependencies](#dependencies) manually.
If a DEB package installation is also present, conf.ini and the profiles will be read from the folder /etc/galicaster. Otherwise, the ones in the installation folder will be used.

> ###### Adding a launcher
You can easilly add a launcher to a manual installation by creating a file at /usr/local/bin/ containing the following command:
```bash
python <path>/run_galicaster.py
```

### Installation

 The Ubuntu Software Center will install the DEB package by simply double-clicking on it. Both the Galicaster software and the dependencies will be installed.

> ￼The Ubuntu Software Center shows a warning because Galicaster does not strictly follow the .deb standards. You can safely ignore it and continue the installation.

You may also run the following command on a shell (needs root permissions):

```bash
dpkg --install <galicaster_$version_all.deb>
```
Galicaster will be installed in `/usr/share/galicaster` . The configuration files and profiles folder will be placed at `/etc/galicaster/`. In order to get Galicaster ready to go, it would be useful running this command to put the right file owners:
```bash
sudo chown -R <user>:<group> /etc/galicaster
```
New profiles can be added in `/etc/galicaster/profiles`. For more information about them, refer to the [Input Profiles section](GalicasterConfiguration/InputProfiles.md).

You may remove Galicaster from your system using the Ubuntu Software Center or the following command on a terminal:
```bash
dpkg --remove galicaster
```
The files at `/etc/galicaster` will not be removed, thus preserving your configuration. If you also want to delete them too, run this instead:

```bash
sudo rm /etc/galicaster/profiles/*.*
sudo dpkg --purge galicaster
```
#### Dependencies

Galicaster depends on the following modules and libraries:

* `python, python-gtk2, libgtk2.0-0`
* `python-gst0.10, libgstreamer0.10-0, gstreamer0.10-plugins-base, gstreamer0.10-plugins-good, gstreamer0.10-plugins-base-apps, gstreamer0.10-ffmpeg, gstreamer0.10-alsa, gstreamer0.10-plugins-bad, gstreamer0.10-plugins-bad-multiverse, gstreamer0.10-plugins-ugly`
* `python-pip, python-setuptools, python-pycurl, python-bottle`
* `v4l-conf, v4l-utils, guvcview`
* `icalendar, phyton-glade2`

For testing devices, specially webcams and V4L2-compatible devices, other software may be installed as well:

* `guvcview (apt)`

### Run Galicaster for the first time
Once installed, Galicaster is ready to run. You may start Galicaster by:

* Opening a terminal and executing galicaster.
* Find Galicaster under Applications in the Unity Menu.
You can also add Galicaster to your Unity sidebar, place a link at the Desktop or include it as a startup application.

The default input Profile consists of two mock video sources and a mock audio source. You can try recording from them, edit its metadata and check if the media is listed in the Media Manager.


### Install drivers
Depending on the hardware you have chosen to run Galicaster with, you may need to install and configure its drivers.

Check our [Compatible hardware](HardwareRecommendations/CompatibleHardware.md) and visit your device manufacturer's Driver & Info websites for information on how to install and configure the drivers.

> If you have purcharsed a Galicaster unit, the drivers are already installed.
