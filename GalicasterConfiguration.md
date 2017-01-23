Galicaster configuration
========================

*This page is updated to the 1.4.2 release*

Configuring Galicaster involves:

* The general configuration of the application - including the Opencast server configuration;
* The setup of different device combinations, known as Input Profiles;
* The activation of certain Plugins.

Due to their their extension and importance, Profiles and Plugins are further explained on their own spaces.

### General configuration
The general configuration file is `conf.ini`, located by default at the directory `/etc/galicaster/` of your system. This file includes several sections regarding:

* [Main parameters](main-parameters), including designated work folders
* [Logger](logger)
* [Opencast server configuration](opencast-server-configuration)
  * [Heartbeat configuration](heartbeat-configuration): frequency of communication signals
  * [Series configuration](series-configuration)
* [Plugins configuration](GalicasterConfiguration/Plugins.md)

> `conf-dist.ini`
> The file `conf-dist.ini`, located at the installation folder of Galicaster, contains the factory configuration of Galicaster. You can check the default parameters there. This file is meant to remain unchanged.


### Main parameters
Parameters are set in different sections at the `conf.ini file`. Parameters include folder designation, UI configuration, processing options, etc.

In the `basic` section of the `conf.ini` file, you can configure the following items:

* [Administration mode](administration-mode)
* [Active profile](active-profile) - configurable through the interface
* [Stop dialog](stop-dialog)
* [Quit option](quit)
* [Shutdown option](shutdown)
* [Resolution](resolution)

#### Administration mode
The *admin mode* allows the user to access the Profile Selector and the Media manager. If the *admin mode* is disabled, only the Recorder area is available and the selected profile is locked.

> [basic]
> admin = True|False

Default value: `True`


#### Active profile
The active profile is saved in the `conf.ini` file. Use the Profile Selector in the graphical interface to change it.

> [basic]
> profile = Default

Default value: `Default`

#### Stop dialog
If set, an "are you sure" pop-up will show when the stop button is clicked during a recording. If unset, the recording will stop immediatly.
Disabling this option is specially useful in consecutive recordings, where the time between pieces is minimum.

> [basic]
> stopdialog = True|False

Default value: `False`

#### Quit
If set, a "Quit" button will be displayed in the Welcome screen of Galicaster. The quit button will close Galicaster.
If shortcuts are activated, the program can be closed with ctrl+shift+q

> [basic]
> quit = True|False

Default value: `True`

#### Shutdown
If set, a "Shutdown" button will be displayed in the Welcome screen of Galicaster. The shutdown button will close Galicaster and shutdown the system.

> [basic]
> shutdown = True|False

Default value: `False`

#### Resolution
The application window resolution can be defined manually. Recommended resolutions are 1080p, 1024x768 and 1280x1024. Other resolutions are also possible. "auto" will adapt the resolution to the maximum available in fullscreen mode.

> [basic]
> resolution = auto|1920x1080|1024x768|...

Default value: `auto`

> ￼Dual screens may require a manual resolution to be defined.

#### Swap videos
If set, a button will be displayed in the Recorder view in order to be able to swap the preview videos. For instance, if the camera is been displayed in the right side, pressing this button will be shown in the left side and the screen preview will be shown in the other side.

> [basic]
> swapvideos = True|False

Default value: `True`

#### Side-by-side layout
Three types of layout are provide: Side-by-side and Picture-in-picture with screen or camera as main picture. In future releases the layout will be more customizable.

> [sidebyside]
> layout = sbs

Layout options: (**sbs**|pip-screen|pip-camera)

#### Conflicts between manual and scheduled recordings
Different conflict resolution for manual versus scheduled recordings.

* manual: If active, the user can start manual recordings
* stop: If active and manual unactive, a recording can be stopped.
* start: If activa and manual unactive, a recording can be started.
* pause: whether any recording can be paused.
* overlap : wheter a manual recording can or cannot cancel a scheduled recording.

> [allows]
> manual = True
> start = False
> stop = False
> pause = True

### Media Manager appearance
The Media Manager appearance, more specificaly the color of the row, depends on the Mediapackage status, can be customized. If the classic color is selected, row color depends on the Ingest operation status, otherwise, each operation cell wil acdquire a different color depending on its status.

> [color]
> classic = false
> none =  #FFF0AA ;yellow
> nightly = #AEFFAE ; light green
> pending = #AEFFAE ; light green
> processing = #FFAE00 ; orange
> done = #88FF88 ; green
> failed = #FFAEAE ;red

### Folder designation
#### Repository folder
The main folder and the name format of the subfolders can be modified.

> [basic]
> repository = /path/to/folder/repository/

> [repository]
> foldertemplate = gc_{hostname}_{year}-{month}-{day}T{hour}h{minute}m{second}

Default value: `/home/$user/Repository`
Template format: Free text; the following substitutions (in curly braces) are available: year, month, day, hour, minute, second and hostname.

>	Repository privileges
The default user must have privileges for accessing and writing on this folder, otherwise you can execute a command like this:
`sudo chown -R $user /path/to/folder/repository/`

#### Export Folder
The default user must have privileges for accessing and writing this folder.

>	[basic]
>	export = /path/to/folder/export/

Default value: `/home/$user/_1`

#### Temporary folder
The default user must have privileges for accessing and writing on this folder.

>	[basic]
>	tmp = /path/folder/repository/

Default value: `/tmp` (in Ubuntu distros)

### Logger
By default, the log information is stored at the temporary folder, in a single file named galicaster.log, so the file is deleted on every reboot. However, the syslog system may be used instead. The log level and destination folder can be also configured.

>	[logger]
>	path = /tmp/galicaster.log
>	level = DEBUG
>	use_syslog = False
>	rotate = False

level: (INFO|WARNING|**DEBUG**)
use_syslog: (True|**False**)
rotate: (True|**False**)

### Opencast server configuration
Galicaster can connect to an Opencast core, but certain requirements have to be met:

* A digest user account and password have to be provided. A regular user will not work
* The server has to be reachable by the Galicaster agent. This usually means that both machines have to be in the same network.
* If the Opencast version is previous to 1.4, the legacy mode has to be activated.

#### Scheduled recordings
Scheduled recordings are taken from the Opencast core scheduling system. Any scheduled recording has metadata associated with it and its series. Galicaster will fetch all metadata and allow the user to modify some of them.
Scheduled recordings can be ingested immediately or nightly - the nocturnal ingest time is defined in the heartbeat section - or reingested manually anytime through the media manager.

> [basic]
> scheduled = none|immediately|nightly

#### Manual recordings
Galicaster can set up the default values for some parameters in Manual recordings:

* Workflow
* Workflow parameters
* Ingest schedule

> [basic]
> manual = none|immediately|nightly

#### Galicaster agent hostname
A Galicaster agent registers with a name based on the machine hostname ( `gc-$hostname-[mobile]` ). A customized name can be set up to be used as hostname on the Opencast agent handler.

### Parameters
This is a summary of all the parameters related to the Opencast configuration in Galicaster (default values are displayed in **bold**):

* **active**: Enables the connection to a Opencast server. (True|**False**)
* **manual**: Configure when the manual recordings will be automatically ingested. (**none**|immediately|nightly)
  * **none**: disable automatic ingestion.
  * **immediately**: ingest immediately after the recording.
  * **nightly**: ingest the recordings of the day at night (nightly).
* **scheduled**: Configure when the scheduled recordings will be automatically ingested. (**none**|immediately|nightly)
  * **none**: disable automatic ingestion.
  * **immediately**: ingest immediately after the recording
  * **nightly**: ingest the recordings of the day at night.
* **host**: Opencast server URL (For example:  http://<opencast_server_ip_address>:<opencast_server_port>).
* **username**: Name of the account used to operate the Opencast REST endpoints.
* **password**: Password for the account used to operate the Opencast REST endpoints.
* **hostname**: Name of the Galicaster unit. Defaults to the host name as defined in the OS, prepended by "GC-" if it is a Galicaster Class or "GCMobile-" if it is a Galicaster Mobile.
* **workflow**: name of the workflow used to ingest the recordings.
* **workflow-parameters**: list of name-value pairs (name:value) to be passed to the Opencast workflow. The items in the list are separated by semicolons (";").
  * If you specify trimHold:true you will also need videoPreview:true for the default workflow.
* **legacy**: Whether to use 1.2 & 1.3 Opencast compatibility mode. (True|**False**)
* **visible_tracks**: Whether or not the tracks in Galicaster are visible.(True|**False**)
  * If active, the available tracks are reported to Opencast, so that the user can choose which ones will be recorded.
  * If not, Galicaster will record all the tracks in the profile active at the moment the scheduled recording starts.
    * If this option is active, and the track names in the configuration file are changed for some reason, the previously scheduled recordings may fail because the track names in such recordings will not much the current track names. Therefore, all the existing recordings should be scheduled again if such a change is made.
* **multiple-ingest**: (new in Galicaster 1.3.1): Whether ingestion is made through the admin server or through the less loaded available ingest server. When the option is active, Galicaster looks for the less loaded active sever (not in mantenaince nor offline), always avoiding the admin server. True | **False** (default value) .
* **address**: IP to connect with Opencast.
￼
> Changes in track names
If this option is **_enabled_**, and track names are changed at the configuration file for some reason, the recordings already scheduled in Opencast may fail because the track names in the schedule will not match the current ones. Therefore, if the track names are modified, all the existing recordings should be scheduled again so that they include the new track names.
When this option is **_disabled_**, Galicaster sends no information about the tracks defined in its profile, and therefore no special precautions should be taken when the track names need to be modified for some reason.

#### Example:
> [ingest]
active = True
legacy = False
visible_tracks = False
manual =  nightly
scheduled = immediately
host = http://fakeadmin.matterhorn.com:80
username = matterhorn_system_account
password = CHANGE_ME
workflow = full
workflow-parameters = videoPreview:true;trimHold:true;captionHold:false;archiveOp:true
multiple-ingest = False
address = 127.0.0.1

### Heartbeat configuration
The heartbeat module handles the frequency by which the Opencast communication module in Galicaster send messages to the designated Opencast server.

There are three periodic signals: short period, long period and 24-hour period (night)_

* **short period**: send capture agent status messages.
  * Value in seconds. Default: 10 seconds
* **long period**: check schedule updates.
    * Value in seconds. Default: 60 seconds
* 24-hour period or **night period**: start nightly ingestions.
  * Value in hh:mm format. Default 00:00

#### Default configuration example:
> [heartbeat]
short = 10
long = 60
night = 00:00

### Series configuration
This section sets allows filtering series shown in the drop down list of the metadata editor. It accepts most of the filter values that Opencast endpoint accepts, namely: seriesId, seriesTitle, creator, contributor, publisher, rightsholder, createdfrom, createdto, language, license, subject, abstract, description.

> According to Opencast documentation, the date-like filters (createdfrom and createdto) must follow the format yyyy-MM-dd'T'HH:mm:ss'Z'

In addition to the previous filters, the 'default' keyword accepts a series ID that will appear in the series list, no matter what. The values to the parameters may include placeholders for certain environment variables. The only one supported currently is '{user}', that is substituted with the current user name.

> [series]
default = XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
contributor = {user}
... etc
