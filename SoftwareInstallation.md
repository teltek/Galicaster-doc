Software installation
=====================

*This page is updated to the 2.0.0 release*

Installation process
--------------------
The installation process consists of 5 simple steps:

1. [Check the prerequisites.](#step-1-check-the-prerequisites)
1. [Install the software.](#step-2-install-the-software)
1. [Setup config directory](#step-3-setup-config-directory)
1. [Install and configure drivers.](#step-4-install-and-configure-drivers-optional)( optional )
1. [Run Galicaster for the first time.](#step-5-run-galicaster-for-the-first-time)

After installing Galicaster, the next step is configuring it. You can take a look at the [Configuration Guide](GalicasterConfiguration.md).

### Step 1: Check the prerequisites
Before starting the installation process, please make sure that:

* Your unit meets Galicaster [Hardware Recommendations.](HardwareRecommendations.md)
* You are running a Linux-based OS. The recommended distribution is Ubuntu 16.04. Make sure that the version chosen matches your system architecture (32 or 64 bits). If using the recommended Linux OS, check the following guide: [How to install Ubuntu.](SoftwareInstallation/InstallingUbuntu.md)
* `galicaster` is the default user in the system.

|![forbbiden](images/forbidden.gif) Important                                               |
|                    :------                                             |
|   Due to a [bug in Gstreamer v4l2 library](https://github.com/teltek/Galicaster/issues/298), present in the 1.8.3 version, it is necessary to install our patched version from our repositories, or to compile the latest GStreamer 1.10.3 version manually. We have included the installation of the patched version in our installation instructions. |


### Step 2: Install the software
 There are three options to install Galicaster:
 * [Install through our repository](#using-the-galicaster-repository). This is the recommended option for newcomers.
 * [Download and install DEB package.](#install-from-deb-package)
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
sudo apt-get install gstreamer1.0-plugins-good #Required due to gstreamer error
sudo apt-get install galicaster
```
If you are **upgrading from a previous 2.0-RCX version**, you just need to execute
```bash
sudo apt-get update
sudo apt-get install gstreamer1.0-plugins-good #Required due to gstreamer error
sudo apt-get install galicaster
```

#### Install from .deb package
The latest Galicaster version can be downloaded [here](http://webfiler.teltek.es/webfiler/galicaster/galicaster_2.0.0_all.deb), as a DEB package. Older versions and information about the new features that each of them included are available on the [Release Archive.](SoftwareInstallation/ReleaseArchive.md)

Once downloaded, the DEB package can be installed through the Ubuntu Software Center by simply *double-clicking* on it. Both the Galicaster software and the dependencies will be installed.

|![Info](images/info.gif) Info                                                |
|                    :------                                             |
|   The Ubuntu Software Center will show a warning. You can safely ignore it and continue the installation. This is due to Galicaster not strictly adhering to the Ubuntu .deb standards. |

Alternatively, you may also run the following command on a shell (needs root permissions):

```bash
dpkg --install <galicaster_2.0.0_all.deb>
```

|![Info](images/info.gif) Important                                      |
|                    :------                                             |
|   The patched GStreamer package can be found [here](). The package requires GStreamer 1.8.3. Once downloaded, install it with: <br> `dpkg -i gstreamer1.0-plugins-good_1.8.3-1ubuntu0.3teltek0.1_amd64.deb` |

You may remove Galicaster from your system using the Ubuntu Software Center or the following command on a terminal:
```bash
dpkg --remove galicaster
```
The files at `/etc/galicaster` will not be removed when removing Galicaster, thus preserving your configuration. If you also want to delete them too, run this:

```bash
sudo rm /etc/galicaster/profiles/*.*
sudo dpkg --purge galicaster
```

#### Source code
As an alternative, you can install Galicaster from the source code. Stable versions are available on the [Release Archive.](SoftwareInstallation/ReleaseArchive.md). Stable and development versions, as well as development information, are available in our [Git repository](http://github.com/teltek/Galicaster).

Installing a source code version requires installing its [dependencies](#dependencies) manually.
If a DEB package installation is also present, conf.ini and the profiles will be read from the folder /etc/galicaster. Otherwise, the ones in the installation folder will be used.

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

|![Info](images/info.gif) Info |
| :------ |
| For testing devices, specially webcams and V4L2-compatible devices, other software may be installed as well:<li>`guvcview (apt)`</li><li>`v4l-utils (apt)`</li> |

### Step 3: Setup config directory

Galicaster will be installed in `/usr/share/galicaster` . The configuration files and profiles folder will be placed at `/etc/galicaster/`. In order to editIn order to get Galicaster ready to go, it would be useful running this command to put the right file owners:
```bash
sudo chown -R galicaster:galicaster /etc/galicaster
```

### Step 4: Install and configure drivers (Optional)
Depending on the hardware you have chosen to run Galicaster with, you may need to install and configure its drivers.

Check our [Compatible hardware](HardwareRecommendations/CompatibleHardware.md) and visit your device manufacturer's Driver & Info websites for information on how to install and configure the drivers.

|![Info](images/info.gif) Info                                                |
|                    :------                                             |
|   If you have purchased a Galicaster unit, the drivers are already installed. |

### Step 5: Run Galicaster for the first time
Once installed, Galicaster is ready to run. You may start Galicaster by:

* Opening a terminal and executing `galicaster`.
* Find Galicaster under `Applications` in the Unity Menu.
You can also add Galicaster to your Unity sidebar, place a link at the Desktop or include it as a startup application.

The default Input Profile consists of two mock video sources and a mock audio source. You can try recording from them, edit its metadata and check if the media is listed in the Media Manager.
