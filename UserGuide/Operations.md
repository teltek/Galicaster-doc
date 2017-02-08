Operations
==========

Galicaster is able to perform certain procedures over mediapackages. This procedures are called Operations.

Current operations include:

* [Ingest](#ingest) recordings to a Opencast Matterhorn server.
* Create a [side-by-side](#side-by-side) composition of a video.
* [Export to zip](#export-to-zip)

To perform an operation, select a recording on the Media Manager and click over the Operations button, a dialog will pop-up with the available operation for the chosen content.

Operations are resolved sequentially in order of assigment. Alternativally, operation can be enqueued to be resolved nightly so it wouldn't interfire with recording matters. In that case, operations can be cancelled by opening the dialog again and selecting the respecive button.


### Ingest
*Ingest* is the operation that sends the recordings to the publishing platform.

Ingestion requires network access and some configuration data indicating parameters of the server to connect. *Ingest* will not be available if:

* The server configuration is wrong.
* The connection is disabled.
* The network is down.
* The server is down.
* The server is unreachable.

Once ingested, a recording can be re-ingested, but it will probably overwrite the previous one if you do it in the same server.


### Export to Zip
*Export to zip* will gather all the recording streams and metadata files into a single uncompressed zip file. The zip package will be placed on the zip designated folder, by default the user Home folder (i.e. `/home/user/`).


### Side by Side
*Side by side* operation exports a mediapackage streams to a single file. Once finished the resulting file will be placed on the sidebyside designated folder, by default the user Home folder (e.g. `/home/user/`).

*Note: Side by Side operation is still in beta phase, it only works on mediapackages with two video streams. Otherwise the operation will fail.*
