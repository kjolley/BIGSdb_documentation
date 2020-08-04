.. _versioning:

*************************
Isolate record versioning
*************************
Versioning enables multiple versions of genomes to be uploaded to the database 
and be analysed separately.  When a new version is created, a copy of the 
provenance metadata, and publication links are created in a new isolate record.
The sequence bin and allele designations are not copied.

By default, old versions of the record are not returned from queries.  Most 
query pages have a checkbox to 'Include old record versions' to override this.

Links to different versions are displayed within an isolate record:

.. image:: /images/curation/versions.png

The different versions will also be listed in analysis plugins, with old 
versions identified with an [old version] designation after their name.

To create a new version of an isolate record, query or browse for the isolate:

.. image:: /images/curation/versions2.png

Click the 'create' new version link next to the isolate record:

.. image:: /images/curation/versions3.png

The isolate record will be displayed.  The suggested id number for the new 
record will be displayed - you can change this.  By default, the new record 
will also be added to any projects that the old record is a member of.  
Uncheck the 'Add new version to projects' checkbox to prevent this.

Click the 'Create' button.

.. image:: /images/curation/versions4.png
