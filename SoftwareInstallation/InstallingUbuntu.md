Installing Ubuntu
=================

*This document is updated to the 2.0.0 release*

1. Download Ubuntu 16.04.2  

  * The recommended distribution is Ubuntu 16.04.2, following this link you can download the refered distribution [Ubuntu 16.04.2](http://releases.ubuntu.com/16.04/)

2. Install Ubuntu 16.04.2
  1. Mark the field `install this third-party software`
  2. Don't select the field `Download updates while installing`
  3. Use `galicaster` as the default user. **This is mandatory.**

3. Once the installation of Ubuntu is done, it's necessary to install:
```bash
sudo apt remove  xserver-xorg-core-hwe-16.04
sudo apt install ubuntu-desktop xorg xserver-xorg-core #Fix #543
```

4. Now you can [install Galicaster](../SoftwareInstallation.md)
