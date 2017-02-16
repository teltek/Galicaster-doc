Software installation
=====================

*This page is updated to the 2.0.0 release*

Installation process
--------------------
The installation process consists of 5 simple steps:

* [Check the prerequisites.](#prerequisites)
* [Install the software.](#installation)
* [Setup config directory](#setup-config-directory)
* [Install and configure drivers.](#install-drivers)( optional )
* [Run Galicaster for the first time.](#run-galicaster-for-the-first-time)

After installing Galicaster, the next step is configuring it. You can take a look at the [Configuration Guide](GalicasterConfiguration.md).

### Prerequisites
Before starting the installation process, please make sure that:

* Your unit meets Galicaster [Hardware Recommendations.](HardwareRecommendations.md)
* You are running a Linux-based OS. The recommended distribution is Ubuntu 16.04. Make sure that the version chosen matches your system architecture (32 or 64 bits). If using the recommended Linux OS, check the following guide: [How to install Ubuntu.](SoftwareInstallation/InstallingUbuntu.md)
* `galicaster` is the default user in the system.

### Installation
 There are three options to install Galicaster:
 * [Install through our repository](#using-the-galicaster-repository). This is the recommended option for newcomers.
 * [Clone the source code and install manually.](#source-code)


 By installing or downloading Galicaster, you agree to the [non-commercial license](http://creativecommons.org/licenses/by-nc-sa/3.0/). ![](http://i.creativecommons.org/l/by-nc-sa/3.0/80x15.png) (Commercial licenses also available under request)

#### Using the Galicaster repository
Installation instructions using the galicaster repository are as follows:

|![Info](images/info.gif) Info                                                |
|                    :------                                             |
|   Remember to install the system using the galicaster user|

```bash
echo "deb https://packages.galicaster.org/apt xenial main" | sudo tee --append /etc/apt/sources.list.d/galicaster.list
wget -O - https://packages.galicaster.org/apt/galicaster.gpg.key  | sudo apt-key add -
sudo apt-get update
sudo apt-get install galicaster
```
If you are **upgrading from a previous 2.0 version**, you just need to execute
```bash
sudo apt-get update
sudo apt-get install galicaster
```

#### Source code
As an alternative, you can install Galicaster from the source code. Stable versions are available on the [Release Archive.](SoftwareInstallation/ReleaseArchive.md). Stable and development versions, as well as development information, are available in our [Git repository](http://github.com/teltek/Galicaster).

Installing a source code version requires installing its [dependencies](#dependencies) manually.
If a repository installation is also present, conf.ini and the profiles will be read from the folder /etc/galicaster. Otherwise, the ones in the installation folder will be used.

##### Dependencies

Galicaster depends on the following modules and libraries:
```
python python-pip python-setuptools python-pycurl python-bottle python-glade2 python-icalendar python-gi python-dbus python-simplejson
gstreamer1.0-plugins-base gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-plugins-good gstreamer1.0-alsa gstreamer1.0-libav
gir1.2-gstreamer-1.0 gir1.2-gtk-3.0 gir1.2-gst-plugins-base-1.0
onboard onboard-data
```

###### Adding a launcher
You can easilly add a launcher to a manual installation by creating a file at `/usr/local/bin/` containing the following command:
```bash
python <path>/run_galicaster.py
```
where `<path>` is the directory where you downloaded galicaster source code.

|![Info](images/info.gif) |
| :------ |
| For testing devices, specially webcams and V4L2-compatible devices, other software may be installed as well:<li>`guvcview (apt)`</li><li>`v4l-utils (apt)`</li> |

### Setup config directory

Galicaster will be installed in `/usr/share/galicaster` . The configuration files and profiles folder will be placed at `/etc/galicaster/`. In order to editIn order to get Galicaster ready to go, it would be useful running this command to put the right file owners:
```bash
sudo chown -R galicaster:galicaster /etc/galicaster
```

### Install drivers
Depending on the hardware you have chosen to run Galicaster with, you may need to install and configure its drivers.

Check our [Compatible hardware](HardwareRecommendations/CompatibleHardware.md) and visit your device manufacturer's Driver & Info websites for information on how to install and configure the drivers.

|![Info](images/info.gif) Info                                                |
|                    :------                                             |
|   If you have purchased a Galicaster unit, the drivers are already installed. |

### Run Galicaster for the first time
Once installed, Galicaster is ready to run. You may start Galicaster by:

* Opening a terminal and executing `galicaster`.
* Find Galicaster under `Applications` in the Unity Menu.
You can also add Galicaster to your Unity sidebar, place a link at the Desktop or include it as a startup application.

The default Input Profile consists of two mock video sources and a mock audio source. You can try recording from them, edit its metadata and check if the media is listed in the Media Manager.


