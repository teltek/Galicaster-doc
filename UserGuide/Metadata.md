Metadata
========

*This page is updated to the 2.0.2 release*

Metadata is the information related to the audivisual content on a recording. The metadata and content together forms a Mediapackage. In the Galicaster repository each folder represents a Mediapackage. Metadata is stored permanently on XML files. **These files should not be edited directly**.

The Galicaster metadata scheme is based on the [Matterhorn Metadata Scheme](https://opencast.jira.com/wiki/pages/viewpage.action?pageId=14614561), and it is based on the Dublin Core initiative.

### Metadata edition
Metadata can be edited on different stages of the recording/Mediapackage cycle of life.

1. On scheduled recordings, on the schedule manager in Opencast Matterhorn
2. During a recording, clicking on Edit Metadata.
3. On the Media Manager, anytime.
4. After ingesting, back in Opencast Matterhorn

Galicaster only allows editing some Metadata: title, presenter, description, language and series. If the series is changed, all the metadata related with series is changed too (series title, series description, series creators ...).


### Custom fields
If your Opencast Matterhorn installation has custom metadata fields, they will be retrieved and keep unchanged by Galicaster, unless they are modified manually or the Series is changed - the lattest only affecting series metadata.

For more information on Metadata and Mediapackagest consult the [Matterhorn Metadata Scheme](https://opencast.jira.com/wiki/pages/viewpage.action?pageId=14614561).
