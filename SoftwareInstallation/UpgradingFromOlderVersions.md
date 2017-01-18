Upgrading from older versions
=============================

### From 1.3.x to 1.4.x
The Galicaster recordings repository doesn't change from 1.3.x to 1.4.x. The only difference is the new dependency `python-glade2`, used for internationalization. To do a manual installation of this new library you only have to execute:

```bash
$ sudo apt-get install --yes python-glade2
```
If you use the deb package, the system installs the new dependency automatically.

The data saved in `Repository/attach/series.json` is different in this Galicaster version. You must remove it to avoid a Galicaster issues when you list the Matterhorn series.

### From 1.2.x to 1.3.x
Galicaster 1.2.x repository is readable by a Galicaster 1.3.0 but not the other way around. If a Mediapackage is created or modified in Galicaster 1.3.0 it won't be seen by a Galicaster 1.2.x due to differences on the Mediapackage metadata files.

Regarding configuration, Galicaster is compatible with 1.2.x configuration. A number of new variables have appeared which are present in the `conf-dist.ini` file:

* shutdown in section admin, to activate a shutdown system button on the UI.
* logger section.
* legacy on section ingest, for Matterhorn 1.2 and 1.3 compatibility.
* visible_tracks on section ingest, for scheduling purposes.

For more information about these and other parameters consult [Galicaster configuration]().

### From 1.1.x to 1.2.0
**The following upgrade steps are optional.** All 1.1 configuration is kept the same, except for the automatic ingest options. However, new variables (which will obviously not appear in the old configuration files) will take default values, which may not be the ones desired.

* Ingest options
  * Automatic mechanisms for ingestion are now splitted in two groups: manual or scheduled recordings
  * Each group can be set to be ingested automatically, immediately or nightly. Consult the [configuration guide]() on ingesting.
* Repository
    * Mediapackages have now three operations, to preserve the status of *ingest* execute the script `docs/scripts/migrate_repository.py`. You have to copy it on the `galicaster` folder before running. Do **not** use it directly in the `Repository` folder.
    * Alternatively, you can create a new repository for 1.2 alone.
* Profiles
    * A profile is a track list with a name to identify it.
    * If no profile is set, the default one will be assumed – the list of active tracks on conf.ini or conf-dist.ini
    * However, you should copy the active tracks into a profile and use it instead the default.
    * Create different profiles depending on the capturing devices available. Use short identifiable names.
    * Take a look at the [profile guide]() to know more about them.
* Export Folder
  * *Export to zip* and Side by side operations leave the resulting file in a [designated folder](). If not specified, the files will be stored at the user home folder, e.g. /home/user/.

### From 1.0.x to 1.1.0
1. The configuration file `conf.ini` must be reviewed. Copy its values into the default `conf-dist.ini` and `conf.ini` and check the [documentation]() for any doubt.
2. New values on the configuration files are: quit option on screen, plugin activation, screensaver inactivity timer and workflow parameters.
If you are using Hauppauge cards, you must set up the vumeter and the playback.
3. As for the Repository, don't worry, you can keep your old recordings intact. You may want to set the series.
4. If you have any recordings scheduled on your Matterhorn core, **use a new Repository** with your Galicaster 1.1 agent. Keep the same name and capabilities (traks) in the agent configuration after your update.

### From 1.0.0 to 1.0.1
This upgrade requires no special changes.
