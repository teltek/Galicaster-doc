
Release Archive
===============

### Galicaster 1.4.2 - 2015 22th June
[Source](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.4.2.tar.gz) - [Debian Package](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.4.2_all.deb) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)

* Add compatibility to use Opencast 1.6 and 2.0.x
* Change in the default videoencoder due to better multicore capabilities of x264enc
* Use calendar response etags to optimize requests. (Issue #64)
* New plugin (notifycrash) to send an email when a recording has failed
* Added an endpoint to close Galicaster through the rest API
* Added the option to configure the output framerate using Blackmagic devices
* Fixed bugs (See all of them in [Github CHANGELOG](https://github.com/teltek/Galicaster/blob/1.4.x/CHANGELOG)
------------------------------------------------------------------------------------
### Galicaster 1.4.1 - 2014 18th August
[Source](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.4.1.tar.gz) - [Debian Package](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.4.1_all.deb) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)

* New retry to recreate the pipeline periodically when a stream dies.
* Fixed enable pause in datapath bin.
* New failovermic plugin
* Fixed initialize plugins before loading modules
* Fixed bug in capture.cleaner.mindiskspace value (Added get_free_space in the repository).
* Added ca_parameters to allow editing of the CA configurations.
* New plugin to reingest recordings where the ingest has failed. (ppettit)
* New screen device module to record the screencast. (olabri)
* New autoaudio device module to automatically detect audio source and sink. (oaubert)
* Using autoaudiosink instead of hardcoding pulsesink in player. (oaubert)
------------------------------------------------------------------------------------
### Galicaster 1.4.0 - 2014 9th April
[Source](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.4.0.tar.gz) - [Debian Package](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.4.0_all.deb) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)

* Source - Debian Package - Installation guide - Configuration
* Feature: Allow configuration of MHHTTPClient timeouts (ppettit)
* Fixed bug: Allow any case for plugin config values (JamesUoM)
* Fixed bug: Set recording state on matterhorn server when doing manual recording (ppettit)
* New rtpraw device module to record re-encoded RTP flow.
* Fixed Bug with relative log and i18n paths.
* Galicaster UI internationalization.
* New plugin (hidetabs) to customize the tabs displayed on the recording UI.
* New plugin (setuprecording) to enter a manual recording's metadata before starting it, set default values and mark some fields as required.
* First version of "hide operations" feature (still in development).
* A button in the recorder UI to swap the video streams, so that the user can customize where are they shown in the preview.
* Fixed bug: Galicaster doesn't crash anymore when a webcam is unplugged. Now you can go back and reload the profile.
* Fixed bug on forced users to click twice in pop-ups when using distributions like Xubuntu.
* Corrected some bad interactions between the no-audio dialog and other popups.
------------------------------------------------------------------------------------
### Galicaster 1.3.2 - 2014 25th March
[Source](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.3.2.tar.gz) - [Debian Package](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.3.2_all.deb) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)

* Fixed bug: Galicaster crashes from python / libgdk errors

------------------------------------------------------------------------------------
### Galicaster 1.3.1 - 2014 20th January
[Source](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.3.1.tar.gz) - [Debian Package](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.3.1_all.deb) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)
* Ingest to a Opencast Matterhorn cluster with multiple ingest servers.
* New Pushpic plugin: send screenshoots periodically for monitoring with Galicaster Dashboard
* Added logstale in REST endpoing plugin.
* Improved VU-meter dynamic range
* Several fixes and bug fixes including:
  * Fixes on dialog modality and focus.
  * Bug on No-audio-dialog when reloading a profile.
  * Fixed serious bug that crashed GC when using Datapath capture cards
------------------------------------------------------------------------------------
### Galicaster 1.3.0 - 2013 27th June
[Source](http://webfiler.teltek.es/webfiler/galicaster/galicaster-1.3.0.tgz) - [Debian Package](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.3.0_all.deb) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)

* Support for RTP sources and Datapath cards
* New Custom device module
* Executable scripts for device configuration on profile loading
* Configurable Encoders and muxers
* Optional Shutdown button on the interface
* Improvements include:
  * Ruled VU meter.
  * Configurable side-by-side layout.
  * New pop-up decoration.
  * Configurable UI resolution.
  * Configurable logger
* Plugins
  * New Check_Repository_plugin: To start missed scheduled recordings on startup.
  * Screen_Saver_Plugin: improved screensaver control for Ubuntu 12.04.
  * No_audio_dialog_plugin: general improvement, more configurable.
------------------------------------------------------------------------------------
### Galicaster 1.2.3 - 2012 December 19
[Source](http://webfiler.teltek.es/webfiler/galicaster/galicaster-1.2.3.tar.gz) - [Debian Package](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.2.3_all.deb) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)

* Feature: After crash partial recordings are saved
* Fix: Minor bug on firewire plugin concerning configuration
* Fix: Minor bug on MH compatibility towards 1.4
------------------------------------------------------------------------------------
## Galicaster 1.2.2 - 2012 November 28
[Source](http://webfiler.teltek.es/webfiler/galicaster/galicaster-1.2.2.tar.gz) - [Debian Package](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.2.2_all.deb) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)

* Opencast-Matterhorn 1.4 Compatible
* Custom template for recording folders

Fixes and bugs:
* XML Namespace can be removed to provide 1.2 and 1.3 MH compatibility
* Metadata ispartof is now isPartOf
* StartTime fixed on manual recordings
* Some fixes on MH Series fetching
------------------------------------------------------------------------------------
### Galicaster 1.2.1 - 2012 October 9
[Source](http://webfiler.teltek.es/webfiler/galicaster/galicaster-1.2.1.tgz) - [Debian Package](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.2.1_all.deb) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)

* Zip Mediapackger larger than 4 GB.
* Side by Side supports embedded audio.
* Fetch upto 100 MH Series.
* Fully Compatible with Ubuntu 10.10.
* Improvements and fixes on audio-based device plugin.
* Fixes related to dialog pop-up.
------------------------------------------------------------------------------------
### Galicaster 1.2.0 - 2012 August 23
[Source](http://webfiler.teltek.es/webfiler/galicaster/galicaster-1.2.0.tgz) - [Debian Package](http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.2.0_all.deb) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)

* Input Profiles
* New Operations: Zip and Side by Side Beta
  * Immediate and nocturne triggering
  * Queue
* Improved Blackmagic cards support
* Improved and configurable OC-Matterhorn messaging
* More information added on Recorder and Media Manager
* Support for more than 2 video streams on preview and playback
* Recorder errors captured
* Bug fixing including:
    * Pycurl bug fix included
    * GTK assertion bug fix include
    * Improved resizing for various resolutions
* Runs on Ubuntu 12.04 LTS
------------------------------------------------------------------------------------
### Galicaster 1.1.1 - 2012 April 27
[Download](http://webfiler.teltek.es/webfiler/galicaster/galicaster-1.1.1.tgz) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)

* Bug fixes

------------------------------------------------------------------------------------
### Galicaster 1.1.0 - 2012 April 12
[Download](http://webfiler.teltek.es/webfiler/galicaster/galicaster-1.1.0.tgz) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)

* Features: Screensaver control, Pausable recordings
* Opencast Matterhorn: Series harvest and editon, Device selection enabled, Workflow parameters enabled
* Several bugs fixed and minor improvements
------------------------------------------------------------------------------------
### Galicaster 1.0.1 - 2012 March 15
[Download](http://webfiler.teltek.es/webfiler/galicaster/galicaster-1.0.1.tgz) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)

* Compatible with Opencast Matterhorn 1.3

------------------------------------------------------------------------------------
### Galicaster 1.0 - 2011 December 22
[Download](http://webfiler.teltek.es/webfiler/galicaster/galicaster-1.0.0.tgz) - [Installation guide](../SoftwareInstallation.md) - [Configuration](../GalicasterConfiguration.md)
