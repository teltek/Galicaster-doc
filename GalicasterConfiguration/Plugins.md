Plugins
=======

*This page is updated to the 2.0.1 release*

Plugins are independent modules that provide a specific feature to Galicaster without affecting its normal behaviour and can be enabled or disabled separately. They may also have some sort of configuration to control its behaviour.
Plugins communicate with Galicaster in a very simple way, by connecting to the inner signals of the program. They also can retrieve information from different elements of the application - repository, profiles, network status, GUI, etc.

The following list enumerates the current available plugins at the 2.0.0 release. Each plugin's functionality and configuration are briefly explained on its corresponding section in this page.

* [Screensaver for Ubuntu 16.04](#screensaver-for-ubuntu-1604)
* [No Audio Warning Dialog](#no-audio-warning-dialog)
* [Hide cursor and modify Ubuntu appearance](#hide-cursor-and-modify-ubuntu-appearance)
* [Check for a non-started scheduled recording](#check-for-a-non-started-scheduled-recording)
* [Clean old recordings](#clean-old-recordings)
* [Limit recording duration](#limit-recording-duration)
* [REST interface (Experimental)](#rest-interface-experimental)
* [Keyboard Shortcuts (Discontinued)](#keyboard-shortcuts-discontinued)
* [Setup the default values of any recording](#setup-the-default-values-of-any-recording)
* [Hide tabs in the recorder UI](#hide-tabs-in-the-recorder-ui)
* [Hide operations](#hide-operations)
* [Send snapshot to Dashboard (Experimental)](#send-snapshot-to-dashboard-experimental)
* [Retry failed ingest](#retry-failed-ingest)
* [On-screen Keyboard](#on-screen-keyboard)
* [Lock Galicaster](#lock-galicaster)
* [Occlude tracks](#occlude-tracks)

### Screensaver for Ubuntu 16.04
This plugin uses the Xorg system and the DBUS application interface to provide an automatic screensaver control for Galicaster. In order to work properly, this plugin requires both the screensaver and tge power management system to be disabled.

#### Behaviour
* Disables the screensaver when a recording is active.
* Enables the screensaver when no recordings are active.
  * The screensaver is displayed after a certain **inactivity** time (in seconds). The value of `inactivity` is configurable.
  * The screensaver stops on keyboard or mouse events (key pressed, mouse movements or clicks), or by touching the screen on a tactile monitor, and the inactivity timer is restarted.
* The screensaver is disabled one minute before a scheduled recording starts. If the screensaver was active at that time, it stops, and the main Galicaster UI is displayed without any external interaction.

#### Loading and configuration:
In `conf.ini` (link to conf.ini), include the following sections with your values of choice:

```ini
[plugins]
screensaver = True

[screensaver]
inactivity = 60
```

`True`: *Enables plugin.*  
`False`: *Disables plugin.*  
`inactivity`: *Length of the inactivity period in seconds. Default value: 120 seconds.*


### No Audio Warning Dialog
This plugin triggers a pop-up dialog on the Recorder Area when the audio is muted, the microphone batteries are depleted or the audio is too low.

#### Behaviour:
###### The dialog shows up when:

* An audio recording device is muted.
* An audio recording device does not have enough power or battery charge.
* The audio input level is too low. The threshold is configurable and defaults to -80dB (see the configuration section for details).

###### The dialog hides when:

* The audio input level goes +5dB above the configured threshold.
* The "Close" button is clicked. It will stay closed until the audio level goes over the threshold and falls again.
* (Disabled by default) The "Keep Closed" button is clicked. The dialog will remain closed, regardless the audio level, until:
  * A new recording is started.
  * The current recording is stopped.
  * A new profile is loaded.
  * The current profile is reloaded.

#### Loading and configuration:
In `conf.ini` (link to conf.ini), include the following sections with your values of choice:

```ini
[plugins]
noaudiodialog = True

[audio]
min = -80
keepclosed = False
```

`True`: *Enables plugin*.  
`False`: *Disables plugin.*  
`min`: *A negative integer representing the 'silence' level in dB. Accepted values range between -100 and 0. Normal values are between -100 and -60. Defaults to -80.*

### Hide cursor and modify Ubuntu appearance
This plugin hides de Ubuntu Unity bar, removes the desktop workspaces and disables Ubuntu desktop lock. Also could hide the mouse cursor.

#### Loading
In `conf.ini` (link to conf.ini), include the following section with your value of choice:

```ini
[plugins]
appearance = False

[appearance]
hidecursor = False
```
`True`: *Enables plugin.*  
`False`: *Disables plugin.*  
`hidecursor`: *Enable or disable cursor*

### Check for a non-started scheduled recording
If the Galicaster unit is turned on after a scheduled recording should had been started, the recording will be lost. This pluging helps mitigating this problem by checking for a recording that should have already been started and starting it immediately for the remaining time.

#### Behaviour
The plugin looks for recordings that should be currently running. If there is any, it is started immediately with its metadata - duration and start time - modified appropriately. The recovered recording will run for the remaining time only. An example:

* Recording scheduled from 10am to 12am.
* Computer started at 10:20.
* The recording will run from 10:20 to 12:00, resulting on a video 1 hour and 40 minutes long.

#### Loading
In `conf.ini` (link to conf.ini), include the following code with your values of choice:

```ini
[plugins]
checkrepo = True
```
`True`: *Enables plugin.*  
`False`: *Disables plugin.*


### Clean old recordings
This plugin deletes every recording older than a certain threshold. It is meant to keep enough free space on the hard drive, assuming the copies of the media in the recording units are not used as backup.

#### Loading and configuring
In `conf.ini` (link to conf.ini), include the following code with your values of choice:

```ini
[plugins]
cleanstale = True

[cleanstale]
maxarchivaldays = 30
checkoninit = False
```
`True`: *Enables plugin.*  
`False`: *Disables plugin.*  
`maxarchivaldays`: *An integer representing number of days the recording will be kept. Defaults to 30.*  
`checkoninit`: *Run the plugin when galicaster starts*

Note: This plugin will execute the process to delete on the hour configured as "nightly" in the section "heartbeat"

### Limit recording duration
This plugin is meant to stop manualkeyboard recordings missed by the lecturer.

#### Behaviour
All recordings stop when they reach the maximum duration configured.

#### Loading and configuring
In `conf.ini` (link to conf.ini), include the following code with your values of choice:

```ini
[plugins]
forcedurationrec = True

[forcedurationrec]
duration = 240
```
`True`: *Enables plugin.*  
`False`: *Disables plugin.*  
`duration`: *An integer representing the maximum duration allowed for a recording, in minutes. Defaults 240 minutes (4 hours).*


### REST interface (Experimental)
This plugin provides a simple REST web interface to retrieve information or control some actions on a running Galicaster instance.
This module requires the installation of the additional package `python-bottle`.

The available endpoints are:

* /state: Show several state values.
* /repository: List all the recordings.
* /repository/<id>: Get the manifest of the MediaPackage with the ID <id> in XML format.
* /metadata/<id>: Get the manifest of the MediaPackage with the ID <id> in JSON format.
* /start: Start a manual recording.
* /stop: Stop current recording.
* /operation/ingest/<id>: Ingest the MediaPackage with ID <id>.
* /operation/sidebyside/<id>: Export the MediaPackage with ID <id> as a side-by-side composition.
* /operation/exporttozip/<id>: Export the Mediapackage with ID <id> as a ZIP file.
* /screen: Get a screenshoot of the active screen
* /logstale: Check if log is stale
* /quit: Quit Galicaster.
  * *Use method __POST__*
* /enable_input: Enable multimedia inputs
  * *Use method __POST__*
  * `Content-Type: application/json`
  * `{"input":[]}`: Enables all inputs
  * `{"input":["Pulse","Webcam"]}`: Enable selected inputs
* /disable_input: Disable multimedia inputs
  * *Use method __POST__*
  * `Content-Type: application/json`
  * `{"input":[]}`: Disables all inputs
  * `{"input":["Pulse","Webcam"]}`: Disable selected inputs
* /enable_preview: Enable preview
  * *Use method __POST__*
  * `Content-Type: application/json`
  * `{"input":[]}`: Enables all previews
  * `{"input":["Pulse","Webcam"]}`: Enable selected previews
* /disable_preview: Disable preview
  * *Use method __POST__*
  * `Content-Type: application/json`
  * `{"input":[]}`: Disable all previews
  * `{"input":["Pulse","Webcam"]}`: Disable selected previews

The REST server is listening in the port 8080 in all interfaces.
It can be accessed via localhost:8080 when the application is running.

```ini
[plugins]
rest = False

[rest]
port = 8080
```

`True`: *Enables plugin.*  
`False`: *Disables plugin.*


### Keyboard Shortcuts (Discontinued)
This plugin captures certain key combinations to trigger specific actions in Galicaster. The key combinations and their associated actions can be configured by the user. At the present time this plugin provides the possibility to exit typing "Ctrl + Shift + Q".

```ini
[plugins]
shortcuts = True
```
`True`: *Enables plugin.*  
`False`: *Disables plugin.*


### Setup the default values of any recording
#### Behaviour
This plugin defines the keys that will be pre-filled in the metadata when the "REC" button is pressed, these are:

* title: Sets up the default value for the recording title.
* presenter or creator: Sets up the default "Presenter" value.
* description: Sets up the default "Description" value.
* language: Sets up the default "Language" value.
* series, ispartof or isPartOf: Sets up the default "Series" id. The ID must exist, otherwise it will be ignored.

The following "placeholder" may be used in the previous values

* {user}: This string will be substituted by the current Unix login name. For instance: "presenter = {user}" will set up the default presenter value to the current user.

Moreover you can filtering series shown in the drop down list of the metadata editor. It accepts most of the filter values that Matterhorn endpoint accepts, namely: seriesId, seriesTitle, creator, contributor, publisher, rightsholder, createdfrom, createdto, language, license, subject, abstract, description.

According to the Matterhorn documentation, the date-like filters (createdfrom and createdto) must follow the format yyyy-MM-dd'T'HH:mm:ss'Z'. In addition to the previous filters, the 'default' keyword accepts a series ID that will appear in the series list, no matter what.

#### Loading
In `conf.ini`, include the following code with your values of choice:

```ini
[plugins]
setuprecording = True

[setuprecording]
title = Default title
presenter = Someone
...

[series]
default = XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
contributor = {user}
...
```
`True`: *Enables plugin.*  
`False`: *Disables plugin.*


### Hide tabs in the recorder UI
#### Behaviour
The currently available configuration keys are:

* hide: SetA space-separated list of tabs that will be hidden in the record UI. Possible values are: 'events', 'recording' and 'status'.
* default: Name of the tab that will be initially displayed in the UI. Possible values are: 'events', 'recording' and 'status' (unquoted)

#### Loading
In `conf.ini`, include the following code with your values of choice:

```ini
[plugins]
hidetabs = True

[hidetabs]
hide = events
default = recording
```

`True`: *Enables plugin.*  
`False`: *Disables plugin.*

### Hide operations
This plugin gives the possibility to hide any operation in the corresponding pop up in the manager UI. It must be a space-separated list and the possible values for both parameters are: 'ingest', 'exporttozip' and 'sidebyside'.

For example:

```ini
[operations]
hide = ingest
hide_nightly = ingest sidebyside exporttozip
```

### Send snapshot to Dashboard (Experimental)
This plugin fetchs a screenchoot of the window through gtk and sends it with Galicaster's Opencast HTTP client to the Dashboard endpoint. This module can work as a plugin or as a separated application.

```ini
[plugins]
pushpic = True
```

### Retry failed ingest
This plugin looks for ingest operations that has failed in order to retry these operations.

```ini
[plugins]
retryingest = True

[retryingest]
check_published = True
check_after = 300
nightly = True
```

`check_published`: *Check with the Opencast client if the mediapackage already has been published, in this case the plugin will ignore this mediapackage*  
`check_after`: *Time between check processes*  
`nightly`: *Schedule the new operations to be processed nightly, if not will be processed at the moment*  


### On-screen Keyboard
This plugin activates Onboard keyboard to use with Galicaster. It is primarily meant to use with tactile screens.

#### Loading
```ini
[plugins]
keyboard = True
```

### Lock Galicaster
This plugin allow to use Galicaster only by authorized users. It can use a simple password or LDAP to authenticate users.

#### Loading and configuration:
In `conf.ini`, include the following section with your value of choice:

```ini
[plugins]
lockscreen = True

[lockscreen]
password = 1234
authentication = basic
ldapserver = ldap://localhost
ldapserverport = 10389
ldapou = users system
ldapdc =
ldapusertype = cn
enable_quit_button = false

ldap_advanced_bind = False
search_dn = cn=admin,dc=example,dc=com
search_password = admin
base_dn = dc=example,dc=com
group = cn=Users,dc=example,dc=com
filter = (&(sAMAccountName={user})(memberof=cn=Users,dc=example,dc=com))
```

`password`: *Password to unlock Galicaster when basic autentication is in use*  
`authentication`: *Type of authentication: (`basic`|`ldap`)*  
`ldapserver`: *URL for LDAP server*  
`ldapserverport`: *Port for LDAP server*  
`ldapou`: *LDAP Organizational Unit*  
`ldapdc`: *LDAP Domain Component*  
`ldapusertype`:  *User type*   
`enable_quit_button`: *Enable or disable quit button in lockscreen window*  
`ldap_advanced_bind`: *Enable advanced bind, search in the ldap for the user and then try to bind it*  
`search_dn`: *Read-only user's DN, which will be used to authenticate against the LDAP server in order to fetch the user's information.*  
`search_password`: *Read-only user's password, which will be used to authenticate against the LDAP server in order to fetch the user's information.*  
`base_dn`: *Base DN for the directory search*  
`group`: *Group where users are located*  
`filter`: *Custom filter to query the database. If a filter is not provided, the default filter is `(&({ldapusertype}={user})(memberof=cn=Users,dc=example,dc=com))` The `{user}` __will be replace by the user introduced in Galicaster.__*

### Occlude tracks
This plugin gives the possibility to disable tracks in the recording when pressing a button in the recorder.  

#### Behaviour
When the button is pressed, the choosed tracks go black. It's possible select where disable the tracks, only in the preview or in the recording.


#### Loading and configuring
In `conf.ini`, include the following code with your values of choice:
```ini
[plugins]
muteinputs = True

[muteinputs]
mute_on_startup = False
bins = Webcam Pulse
mute_type = input
```
`mute_on_startup`: *Disable tracks on startup*  
`bin`: *Tracks name to disable, __if empty disable all__*  
`mute_type`: *Where to disable tracks (`preview`|`input`)*
