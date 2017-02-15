Pushpic (Experimental)
=====================

**_NOT TESTED WITH GALICASTER 2.X_**  
*This page is updated to the 1.4.2 release*

Creates and send a screenshoot to Dashboard periodically.
---------------------------------------------------------

This plugin is meant to work together with Galicaster Dashboard.

The periodicity is determined by the long period signal of the galicaster.core.heartbeat module, by default 60 seconds. If used as a script, the periodicity is determined by an internal variable (see 'Loading and configuraing as a script').

Every period a screenshoot is made of the active desktop - regardless the application is present or on fullscreen mode. The image is then send to the agent screenshot endpoint.

This plugin can be used with a script present on the Galicaster installation tree at `docs/scripts/run_dashboard_push.py`. To run the script copy it into a location of your choice and establish the path to a Galicaster installation:
- By default the folder is the one of a DEB installation: `/usr/share/galicaster`
- Set the path as an enviromental variable: `GALICASTER_PATH`
- Modify the script to use a custom folder instead of `/usr/share/galicaster`

Loading and configuring as a plugin
-----------------------------------
[See Plugins configuration](../GalicasterConfiguration/Plugins.md#send-snapshot-to-dashboard-experimental)

Running and configuring as a script
-----------------------------------

The script send a picture periodically, by default 60 seconds. Modify the variable sleep_period in the script if you want to change the time between screenshoots.

You can run the script via:

* `python run_dashboard_push.py`
* `./run_dashboard_push.py` **You need execution privileges**

The script functioning is independent of the Galicaster instance running. It will work even when Galicaster is not active.
