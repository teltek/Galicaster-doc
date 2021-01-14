Software installation
=====================

*This page is updated to the 3.0 version*

Installation process
--------------------
The installation process consists of 5 simple steps:

- [Software installation](#software-installation)
  - [Installation process](#installation-process)
    - [Step 1: Check the prerequisites](#step-1-check-the-prerequisites)
    - [Step 2: Install the software](#step-2-install-the-software)
      - [Using the Galicaster repository](#using-the-galicaster-repository)
      - [Source code](#source-code)
        - [Dependencies](#dependencies)
          - [Adding a launcher](#adding-a-launcher)
    - [Step 3: Setup config directory](#step-3-setup-config-directory)
    - [Step 4: Install and configure drivers (Optional)](#step-4-install-and-configure-drivers-optional)
    - [Step 5: Run Galicaster for the first time](#step-5-run-galicaster-for-the-first-time)

After installing Galicaster, the next step is configuring it. You can take a look at the [Configuration Guide](GalicasterConfiguration.md).

### Step 1: Check the prerequisites
Before starting the installation process, please make sure that:

* Your unit meets Galicaster [Hardware Recommendations.](HardwareRecommendations.md)
* You are running a Linux-based OS. The recommended distribution is Ubuntu 20.04. Make sure that the version chosen matches your system architecture (32 or 64 bits). If using the recommended Linux OS, check the following guide: [How to install Ubuntu.](SoftwareInstallation/InstallingUbuntu.md)
* `galicaster` is the default user in the system.

|![forbbiden](images/forbidden.gif) Important                                               |
|                    :------                                             |
|   Due to a [bug in Gstreamer v4l2 library](https://github.com/teltek/Galicaster/issues/298), present in the 1.8.3 version, it is necessary to install our patched version from our repositories, or to compile the latest GStreamer 1.10.3 version manually. We have included the installation of the patched version in our installation instructions. |


### Step 2: Install the software
 There are two options to install Galicaster:
 * [Install through our repository](#using-the-galicaster-repository). This is the recommended option for newcomers.
 * [Clone the source code and install manually.](#source-code)


 By installing or downloading Galicaster, you agree to the [non-commercial license](http://creativecommons.org/licenses/by-nc-sa/3.0/). ![](http://i.creativecommons.org/l/by-nc-sa/3.0/80x15.png) (Commercial licenses also available under request)

#### Using the Galicaster repository
Installation instructions using the galicaster repository are as follows:

|![Info](images/info.gif) Info                                                |
|                    :------                                             |
|   Remember to install the system using the galicaster user|

```bash
echo "deb https://packages.galicaster.org/apt focal main" | sudo tee --append /etc/apt/sources.list.d/galicaster.list
wget -O - https://packages.galicaster.org/apt/galicaster.gpg.key  | sudo apt-key add -
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
apt-get install python3 python3-pip python3-setuptools python3-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-base-apps gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-plugins-good gstreamer1.0-plugins-bad-videoparsers gstreamer1.0-plugins-bad-faad gstreamer1.0-alsa gstreamer1.0-libav gstreamer1.0-pulseaudio libgstreamer1.0-0 gir1.2-gstreamer-1.0 gir1.2-gtk-3.0 gir1.2-gst-plugins-base-1.0 python3-pycurl python3-bottle python3-icalendar python3-gi python3-dbus python3-simplejson python3-ldap python3-gst-1.0 python3-parse python3-pil onboard onboard-data libogg0 libvorbis0a libvorbisenc2 libsasl2-dev libldap2-dev libssl-dev python-is-python3
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
